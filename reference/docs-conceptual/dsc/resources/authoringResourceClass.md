---
ms.date: 07/08/2020
keywords: dsc,powershell,конфигурация,установка
title: Написание пользовательских ресурсов DSC с использованием классов PowerShell
description: В этой статье описывается, как создать простой ресурс, который управляет файлом по указанному пути.
ms.openlocfilehash: 72a828795c29e10ff66f164b8871b0fea7a1e0a8
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2020
ms.locfileid: "92667323"
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a>Написание пользовательских ресурсов DSC с использованием классов PowerShell

> Область применения: Windows PowerShell 5.0

С добавлением классов PowerShell в Windows PowerShell 5.0 появилась возможность определить ресурс DSC, создав отдельный класс. Класс определяет схему и реализацию ресурса, а значит, отдельный MOF-файл создавать не нужно. Кроме того, для ресурса на основе класса используется более простая структура папок, поскольку не требуется папка **DSCResources**.

В ресурсе DSC на основе класса схема определяется как свойства класса, которые можно изменить с помощью атрибутов, указав тип свойства. Ресурс реализуется с помощью методов `Get()` , `Set()` и `Test()` , эквивалентных функциям `Get-TargetResource`, `Set-TargetResource` и `Test-TargetResource` в ресурсе сценария.

С помощью инструкций из этой статьи мы создадим простой ресурс с именем **FileResource** , который управляет файлом по указанному пути.

Дополнительные сведения о ресурсах DSC см. в статье [Создание настраиваемых ресурсов для настройки требуемого состояния Windows PowerShell](authoringResource.md).

> [!Note]
> Универсальные коллекции не поддерживаются в ресурсах на основе классов.

## <a name="folder-structure-for-a-class-resource"></a>Структура папок для ресурса класса

Для реализации настраиваемого ресурса DSC с помощью класса PowerShell создайте указанную ниже структуру папок.
Класс определяется в файле `MyDscResource.psm1`, а манифест модуля — в файле `MyDscResource.psd1`.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        MyDscResource.psm1
        MyDscResource.psd1
```

## <a name="create-the-class"></a>Создание класса

Для создания класса PowerShell необходимо ключевое слово class. Чтобы указать, что класс является ресурсом DSC, используйте атрибут `DscResource()` . Имя класса — это имя ресурса DSC.

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a>Объявление свойств

Схема ресурсов DSC определяется как свойства класса. Необходимо объявить три свойства описанным ниже образом.

```powershell
[DscProperty(Key)]
[string]$Path

[DscProperty(Mandatory)]
[Ensure] $Ensure

[DscProperty(Mandatory)]
[string] $SourcePath

[DscProperty(NotConfigurable)]
[Nullable[datetime]] $CreationTime
```

Обратите внимание, что для изменения свойств используются атрибуты. Значения атрибутов выглядит следующим образом:

- **DscProperty(Key)** : свойство является обязательным. Это свойство является ключом. Значения всех свойств, помеченных как ключи, необходимо объединять для уникальной идентификации экземпляра ресурсов в конфигурации.
- **DscProperty(Mandatory)** : свойство является обязательным.
- **DscProperty(NotConfigurable)** : свойство доступно только для чтения. Свойства с таким атрибутом задаются не конфигурацией, а методом `Get()` (если они есть).
- **DscProperty()** : свойство доступно для настройки, но не является обязательным.

Свойства `$Path` и `$SourcePath` являются строками. `$CreationTime` — это свойство [DateTime](/dotnet/api/system.datetime). Свойство `$Ensure` является перечислением и определяется следующим образом:

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a>Реализация методов

Методы `Get()` , `Set()` и `Test()` эквивалентны функциям `Get-TargetResource`, `Set-TargetResource` и `Test-TargetResource` в ресурсе сценария.

Кроме того, этот код включает вспомогательную функцию `CopyFile()`, которая копирует файл из `$SourcePath` в `$Path`.

```powershell
    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)

        if ($this.ensure -eq [Ensure]::Present)
        {
            if(-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ErrorAction Ignore

        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = New-Object -TypeName System.IO.FileInfo($this.Path)

        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
```

### <a name="the-complete-file"></a>Полный файл

Полный файл класса:

```powershell
enum Ensure
{
    Absent
    Present
}

<#
   This resource manages the file in a specific path.
   [DscResource()] indicates the class is a DSC resource
#>

[DscResource()]
class FileResource
{
    <#
       This property is the fully qualified path to the file that is
       expected to be present or absent.

       The [DscProperty(Key)] attribute indicates the property is a
       key and its value uniquely identifies a resource instance.
       Defining this attribute also means the property is required
       and DSC will ensure a value is set before calling the resource.

       A DSC resource must define at least one key property.
    #>
    [DscProperty(Key)]
    [string]$Path

    <#
        This property indicates if the settings should be present or absent
        on the system. For present, the resource ensures the file pointed
        to by $Path exists. For absent, it ensures the file point to by
        $Path does not exist.

        The [DscProperty(Mandatory)] attribute indicates the property is
        required and DSC will guarantee it is set.

        If Mandatory is not specified or if it is defined as
        Mandatory=$false, the value is not guaranteed to be set when DSC
        calls the resource.  This is appropriate for optional properties.
    #>
    [DscProperty(Mandatory)]
    [Ensure] $Ensure

    <#
       This property defines the fully qualified path to a file that will
       be placed on the system if $Ensure = Present and $Path does not
        exist.

       NOTE: This property is required because [DscProperty(Mandatory)] is
        set.
    #>
    [DscProperty(Mandatory)]
    [string] $SourcePath

    <#
       This property reports the file's create timestamp.

       [DscProperty(NotConfigurable)] attribute indicates the property is
       not configurable in DSC configuration.  Properties marked this way
       are populated by the Get() method to report additional details
       about the resource when it is present.

    #>
    [DscProperty(NotConfigurable)]
    [Nullable[datetime]] $CreationTime

    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)
        if ($this.ensure -eq [Ensure]::Present)
        {
            if (-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ea Ignore
        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = new-object System.IO.FileInfo($this.Path)
        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                 to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
} # This module defines a class for a DSC "FileResource" provider.
```

## <a name="create-a-manifest"></a>Создание манифеста

Чтобы сделать ресурс на основе класса доступным для модуля DSC, необходимо добавить в файл манифеста оператор `DscResourcesToExport`, который указывает модулю, что нужно экспортировать этот ресурс. Наш манифест выглядит следующим образом:

```powershell
@{

# Script module or binary module file associated with this manifest.
RootModule = 'MyDscResource.psm1'

DscResourcesToExport = 'FileResource'

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '81624038-5e71-40f8-8905-b1a87afe22d7'

# Author of this module
Author = 'Microsoft Corporation'

# Company or vendor of this module
CompanyName = 'Microsoft Corporation'

# Copyright statement for this module
Copyright = '(c) 2014 Microsoft. All rights reserved.'

# Description of the functionality provided by this module
# Description = ''

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '5.0'

# Name of the Windows PowerShell host required by this module
# PowerShellHostName = ''
}
```

## <a name="test-the-resource"></a>Тестирование ресурса

Сохранив файлы класса и манифеста в структуру папок, как описано выше, вы можете создать конфигурацию, использующую новый ресурс. Инструкции по запуску конфигурации DSC см. в статье [Активирование конфигураций](../pull-server/enactingConfigurations.md). Следующая конфигурация будет проверять, существует ли файл `c:\test\test.txt`, и, если его нет, копировать файл из `c:\test.txt` (необходимо создать файл `c:\test.txt` перед запуском конфигурации).

```powershell
Configuration Test
{
    Import-DSCResource -module MyDscResource
    FileResource file
    {
        Path = "C:\test\test.txt"
        SourcePath = "c:\test.txt"
        Ensure = "Present"
    }
}
Test
Start-DscConfiguration -Wait -Force Test
```

## <a name="supporting-psdscrunascredential"></a>Поддержка PsDscRunAsCredential

> [Примечание.] **PsDscRunAsCredential** поддерживается в PowerShell 5.0 и более поздних версий.

Свойство **PsDscRunAsCredential** может использоваться в блоке ресурса [конфигураций DSC](../configurations/configurations.md), чтобы указать, что ресурс должен выполняться с указанным набором учетных данных. Дополнительные сведения см. в разделе [Запуск DSC с учетными данными пользователя](../configurations/runAsUser.md).

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a>Требование параметра PsDscRunAsCredential для ресурса или его запрещение

Атрибут `DscResource()` принимает необязательный параметр **RunAsCredential**. Этот параметр принимает одно из трех значений:

- `Optional` **PsDscRunAsCredential** является необязательным для конфигураций, которые вызывают этот ресурс. Это значение по умолчанию.
- `Mandatory` **PsDscRunAsCredential** является обязательным для конфигурации, которая вызывает этот ресурс.
- Конфигурации `NotSupported`, которые вызывают этот ресурс, не могут использовать **PsDscRunAsCredential**.
- `Default` аналогичен `Optional`.

Например, используйте следующий атрибут, чтобы указать, что настраиваемый ресурс не поддерживает использование **PsDscRunAsCredential** :

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="declaring-multiple-class-resources-in-a-module"></a>Объявление нескольких ресурсов класса в модуле

Модуль может определять несколько ресурсов DSC на основе класса. Структуру папок можно создать одним из следующих способов:

1. Определите первый ресурс в файле `<ModuleName>.psm1`, а последующие ресурсы в папке **DSCResources**.

   ```
   $env:ProgramFiles\WindowsPowerShell\Modules (folder)
        |- MyDscResource (folder)
           |- MyDscResource.psm1
              MyDscResource.psd1
        |- DSCResources
           |- SecondResource.psm1
   ```

1. Определите все ресурсы в папке **DSCResources**.

   ```
   $env:ProgramFiles\WindowsPowerShell\Modules (folder)
        |- MyDscResource (folder)
           |- MyDscResource.psm1
              MyDscResource.psd1
        |- DSCResources
           |- FirstResource.psm1
              SecondResource.psm1
   ```

> [!NOTE]
> В приведенных выше примерах можно добавлять любые файлы PSM1 из **DSCResources** в ключ **NestedModules** в файле PSD1.

### <a name="access-the-user-context"></a>Доступ к контексту пользователя

Чтобы получить доступ к пользовательскому контексту из настраиваемого ресурса, можно использовать автоматическую переменную `$global:PsDscContext`.

Например, следующий код пропишет пользовательский контекст, по которому выполняется ресурс, в подробный выходной поток:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>См. также:

[Создание пользовательских ресурсов DSC Windows PowerShell](authoringResource.md)
