---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Отладка ресурсов DSC
ms.openlocfilehash: 30d49768fc2301b5306d0001e157d60e2e991883
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
---
# <a name="debugging-dsc-resources"></a>Отладка ресурсов DSC

> Область применения: Windows PowerShell 5.0

В PowerShell 5.0 в DSC появилась новая функция, позволяющая выполнять отладку ресурса DSC при применении конфигурации.

## <a name="enabling-dsc-debugging"></a>Включение отладки DSC
Перед отладкой ресурса необходимо включить отладку с помощью командлета [Enable-DscDebug](https://technet.microsoft.com/library/mt517870.aspx).
Он принимает обязательный параметр **BreakAll**.

Убедитесь, что отладка включена, вызвав командлет [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) и проверив результат.

Следующие выходные данные PowerShell демонстрируют результат включения отладки:


```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```


## <a name="starting-a-configuration-with-debug-enabled"></a>Запуск конфигурации с включенной функцией отладки
Для отладки ресурса DSC необходимо запустить конфигурацию, вызывающую этот ресурс.
В этом примере мы рассмотрим простую конфигурацию, которая вызывает ресурс [WindowsFeature](windowsfeatureResource.md), чтобы проверить, установлен ли компонент WindowsPowerShellWebAccess:

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```
Скомпилировав конфигурацию, запустите ее, вызвав командлет [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx).
Конфигурация остановится, когда локальный диспетчер конфигураций (LCM) вызовет первый ресурс в конфигурации.
Если используются параметры `-Verbose` и `-Wait`, выходные данные будут содержать строки, которые нужно ввести для запуска отладки.

```powershell
Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach.
Use the following commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```
К этому моменту LCM вызвал ресурс и достиг первой контрольной точки.
Последние три строки выходных данных показывают, как присоединиться к процессу и запустить отладку сценария ресурса.

## <a name="debugging-the-resource-script"></a>Отладка сценария ресурса

Запустите новый экземпляр интегрированной среды сценариев PowerShell.
В консоли введите последние три строки выходных данных `Start-DscConfiguration` в виде команд, заменив `<credentials>` на действительные учетные данные пользователя.
Теперь вы должны увидеть строку приглашения, которая выглядит примерно так:

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

В области сценариев будет открыт сценарий ресурса, и отладчик остановится на первой строке функции **Test-TargetResource** (метод **Test()** ресурса на основе класса).
Теперь вы можете использовать команды отладки в интегрированной среде сценариев для пошагового выполнения сценария ресурса, просмотра значений переменных, просмотра стека вызовов и т. д.
Сведения об отладке в интегрированной среде сценариев PowerShell см. в разделе [Отладка сценариев в интегрированной среде сценариев Windows PowerShell](https://technet.microsoft.com/en-us/library/dd819480.aspx).
Помните, что каждая строка в сценарии ресурса (или классе) устанавливается в качестве точки останова.

## <a name="disabling-dsc-debugging"></a>Отключение отладки DSC

После вызова командлета [Enable-DscDebug](https://technet.microsoft.com/library/mt517870.aspx) все вызовы [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) приведут к запуску отладчика для конфигурации. Чтобы обеспечить нормальную работу конфигураций, необходимо отключить отладку, вызвав командлет [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx).

>**Примечание**. Перезагрузка не меняет состояние отладки LCM. Если отладка включена, после перезагрузки запуск конфигурации по-прежнему будет вызывать отладчик.


## <a name="see-also"></a>См. также
- [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md)
- [Написание пользовательских ресурсов DSC с использованием классов PowerShell](authoringResourceClass.md)