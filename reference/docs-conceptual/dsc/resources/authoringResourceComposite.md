---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Составные ресурсы — использование конфигурации DSC как ресурса
ms.openlocfilehash: ef8d5665e552da01977c2f21a43246c72bb7155f
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954351"
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a>Составные ресурсы: использование конфигурации DSC как ресурса

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

На практике конфигурации часто становятся длинными и сложными — вызывают множество разных ресурсов и задают большое количество свойств. Для решения этой проблемы можно использовать настройку требуемого состояния (DSC) Windows PowerShell как ресурс для других конфигураций. Мы называем это составным ресурсом. Составной ресурс — это конфигурация DSC с возможностью настройки параметров. Параметры конфигурации выступают как свойства ресурса. Конфигурация сохраняется как файл с расширением **.schema.psm1** и применяется вместо MOF-схемы и ресурса сценария в типовом ресурсе DSC (дополнительные сведения о ресурсах DSC см. в статье [Ресурсы настройки требуемого состояния Windows PowerShell](resources.md).

## <a name="creating-the-composite-resource"></a>Создание составного ресурса

В нашем примере создается конфигурация, которая вызывает ряд существующих ресурсов для настройки виртуальных машин. Вместо указания значений для настройки в блоках конфигурации она принимает ряд параметров, которые будут использоваться в блоках конфигурации.

```powershell
Configuration xVirtualMachine
{
    param
    (
        # Name of VMs
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String[]] $VMName,

        # Name of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchName,

        # Type of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchType,

        # Source Path for VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDParentPath,

        # Destination path for diff VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDPath,

        # Startup Memory for VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMStartupMemory,

        # State of the VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMState
    )

    # Import the module that defines custom resources
    Import-DscResource -Module xComputerManagement,xHyper-V

    # Install the Hyper-V role
    WindowsFeature HyperV
    {
        Ensure = "Present"
        Name = "Hyper-V"
    }

    # Create the virtual switch
    xVMSwitch $SwitchName
    {
        Ensure = "Present"
        Name = $SwitchName
        Type = $SwitchType
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check for Parent VHD file
    File ParentVHDFile
    {
        Ensure = "Present"
        DestinationPath = $VHDParentPath
        Type = "File"
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check the destination VHD folder
    File VHDFolder
    {
        Ensure = "Present"
        DestinationPath = $VHDPath
        Type = "Directory"
        DependsOn = "[File]ParentVHDFile"
    }

    # Create VM specific diff VHD
    foreach ($Name in $VMName)
    {
        xVHD "VHD$Name"
        {
            Ensure = "Present"
            Name = $Name
            Path = $VHDPath
            ParentPath = $VHDParentPath
            DependsOn = @("[WindowsFeature]HyperV",
                          "[File]VHDFolder")
        }
    }

    # Create VM using the above VHD
    foreach($Name in $VMName)
    {
        xVMHyperV "VMachine$Name"
        {
            Ensure = "Present"
            Name = $Name
            VhDPath = (Join-Path -Path $VHDPath -ChildPath $Name)
            SwitchName = $SwitchName
            StartupMemory = $VMStartupMemory
            State = $VMState
            MACAddress = $MACAddress
            WaitForIP = $true
            DependsOn = @("[WindowsFeature]HyperV",
                          "[xVHD]VHD$Name")
        }
    }
}
```

### <a name="saving-the-configuration-as-a-composite-resource"></a>Сохранение конфигурации как составного ресурса

Чтобы использовать параметризованную конфигурацию как ресурс DSC, сохраните ее в структуре папок, как и любой другой ресурс на базе MOF, и присвойте имя с расширением **. schema.psm1**. В этом примере мы назовем файл **xVirtualMachine.schema.psm1**. Кроме того, необходимо создать манифест с именем **xVirtualMachine.psd1**, содержащий указанную ниже строку. Он дополняет **MyDscResources.psd1** — манифест модуля для всех ресурсов в папке **MyDscResources**.

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

После выполнения этих действия структура папок должна выглядеть следующим образом:

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

Теперь ресурс можно обнаружить с помощью командлета Get-DscResource, а его свойство — с помощью того же командлета или комбинации клавиш **Ctrl + Space**, активирующей автозаполнение в интегрированной среде сценариев Windows PowerShell.

## <a name="using-the-composite-resource"></a>Применение составного ресурса

Теперь создадим конфигурацию, которая вызывает составной ресурс. Эта конфигурация вызывает составной ресурс xVirtualMachine для создания виртуальной машины, а затем ресурс **xComputer**, чтобы ее переименовать.

```powershell

configuration RenameVM
{

    Import-DscResource -Module xVirtualMachine
    Node localhost
    {
        xVirtualMachine VM
        {
            VMName = "Test"
            SwitchName = "Internal"
            SwitchType = "Internal"
            VhdParentPath = "C:\Demo\VHD\RTM.vhd"
            VHDPath = "C:\Demo\VHD"
            VMStartupMemory = 1024MB
            VMState = "Running"
        }
    }

    Node "192.168.10.1"
    {
        xComputer Name
        {
            Name = "SQL01"
            DomainName = "fourthcoffee.com"
        }
    }
}
```

## <a name="supporting-psdscrunascredential"></a>Поддержка PsDscRunAsCredential

>**Примечание**. **PsDscRunAsCredential** поддерживается в PowerShell 5.0 и более поздних версий.

Свойство **PsDscRunAsCredential** может использоваться в блоке ресурса [конфигураций DSC](../configurations/configurations.md), чтобы указать, что ресурс должен выполняться с указанным набором учетных данных.
Дополнительные сведения см. в разделе [Запуск DSC с учетными данными пользователя](../configurations/runAsUser.md).

Чтобы получить доступ к пользовательскому контексту из настраиваемого ресурса, можно использовать автоматическую переменную `$PsDscContext`.

Например, следующий код пропишет пользовательский контекст, по которому выполняется ресурс, в подробный выходной поток:

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>См. также
### <a name="concepts"></a>Концепции
* [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md)
* [Начало работы с настройкой требуемого состояния Windows PowerShell](../overview/overview.md)