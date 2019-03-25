---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Отладка ресурсов DSC
ms.openlocfilehash: c088e13a25ba31ceebaf52b2d24b5d32b96ae2fc
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2019
ms.locfileid: "58055586"
---
# <a name="debugging-dsc-resources"></a><span data-ttu-id="08cdd-103">Отладка ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="08cdd-103">Debugging DSC resources</span></span>

> <span data-ttu-id="08cdd-104">Область применения. Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="08cdd-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="08cdd-105">В PowerShell 5.0 в DSC появилась новая функция, позволяющая выполнять отладку ресурса DSC при применении конфигурации.</span><span class="sxs-lookup"><span data-stu-id="08cdd-105">In PowerShell 5.0, a new feature was introduced in Desired State Configuration (DSC) that allows you to debug a DSC resource as a configuration is being applied.</span></span>

## <a name="enabling-dsc-debugging"></a><span data-ttu-id="08cdd-106">Включение отладки DSC</span><span class="sxs-lookup"><span data-stu-id="08cdd-106">Enabling DSC debugging</span></span>
<span data-ttu-id="08cdd-107">Перед отладкой ресурса необходимо включить отладку с помощью командлета [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug).</span><span class="sxs-lookup"><span data-stu-id="08cdd-107">Before you can debug a resource, you have to enable debugging by calling the [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) cmdlet.</span></span>
<span data-ttu-id="08cdd-108">Он принимает обязательный параметр **BreakAll**.</span><span class="sxs-lookup"><span data-stu-id="08cdd-108">This cmdlet takes a mandatory parameter, **BreakAll**.</span></span>

<span data-ttu-id="08cdd-109">Убедитесь, что отладка включена, вызвав командлет [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) и проверив результат.</span><span class="sxs-lookup"><span data-stu-id="08cdd-109">You can verify that debugging has been enabled by looking at the result of a call to [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager).</span></span>

<span data-ttu-id="08cdd-110">Следующие выходные данные PowerShell демонстрируют результат включения отладки:</span><span class="sxs-lookup"><span data-stu-id="08cdd-110">The following PowerShell output shows the result of enabling debugging:</span></span>


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


## <a name="starting-a-configuration-with-debug-enabled"></a><span data-ttu-id="08cdd-111">Запуск конфигурации с включенной функцией отладки</span><span class="sxs-lookup"><span data-stu-id="08cdd-111">Starting a configuration with debug enabled</span></span>
<span data-ttu-id="08cdd-112">Для отладки ресурса DSC необходимо запустить конфигурацию, вызывающую этот ресурс.</span><span class="sxs-lookup"><span data-stu-id="08cdd-112">To debug a DSC resource, you start a configuration that calls that resource.</span></span>
<span data-ttu-id="08cdd-113">В этом примере мы рассмотрим простую конфигурацию, которая вызывает ресурс **WindowsFeature**, чтобы проверить, установлен ли компонент WindowsPowerShellWebAccess:</span><span class="sxs-lookup"><span data-stu-id="08cdd-113">For this example, we'll look at a simple configuration that calls the **WindowsFeature** resource to ensure that the "WindowsPowerShellWebAccess" feature is installed:</span></span>

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
<span data-ttu-id="08cdd-114">Скомпилировав конфигурацию, запустите ее, вызвав командлет [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span><span class="sxs-lookup"><span data-stu-id="08cdd-114">After compiling the configuration, start it by calling [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span></span>
<span data-ttu-id="08cdd-115">Конфигурация остановится, когда локальный диспетчер конфигураций (LCM) вызовет первый ресурс в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="08cdd-115">The configuration will stop when the Local Configuration Manager (LCM) calls into the first resource in the configuration.</span></span>
<span data-ttu-id="08cdd-116">Если используются параметры `-Verbose` и `-Wait`, выходные данные будут содержать строки, которые нужно ввести для запуска отладки.</span><span class="sxs-lookup"><span data-stu-id="08cdd-116">If you use the `-Verbose` and `-Wait` parameters, the output displays the lines you need to enter to start debugging.</span></span>

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
<span data-ttu-id="08cdd-117">К этому моменту LCM вызвал ресурс и достиг первой контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="08cdd-117">At this point, the LCM has called the resource, and come to the first break point.</span></span>
<span data-ttu-id="08cdd-118">Последние три строки выходных данных показывают, как присоединиться к процессу и запустить отладку сценария ресурса.</span><span class="sxs-lookup"><span data-stu-id="08cdd-118">The last three lines in the output show you how to attach to the process and start debugging the resource script.</span></span>

## <a name="debugging-the-resource-script"></a><span data-ttu-id="08cdd-119">Отладка сценария ресурса</span><span class="sxs-lookup"><span data-stu-id="08cdd-119">Debugging the resource script</span></span>

<span data-ttu-id="08cdd-120">Запустите новый экземпляр интегрированной среды сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08cdd-120">Start a new instance of the PowerShell ISE.</span></span>
<span data-ttu-id="08cdd-121">В консоли введите последние три строки выходных данных `Start-DscConfiguration` в виде команд, заменив `<credentials>` на действительные учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="08cdd-121">In the console pane, enter the last three lines of output from the `Start-DscConfiguration` output as commands, replacing `<credentials>` with valid user credentials.</span></span>
<span data-ttu-id="08cdd-122">Теперь вы должны увидеть строку приглашения, которая выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="08cdd-122">You should now see a prompt that looks similar to:</span></span>

```powershell
[TEST-SRV]: [DBG]: [Process:9000]: [RemoteHost]: PS C:\DebugTest>>
```

<span data-ttu-id="08cdd-123">В области сценариев будет открыт сценарий ресурса, и отладчик остановится на первой строке функции **Test-TargetResource** (метод **Test()** ресурса на основе класса).</span><span class="sxs-lookup"><span data-stu-id="08cdd-123">The resource script will open in the script pane, and the debugger is stopped at the first line of the **Test-TargetResource** function (the **Test()** method of a class-based resource).</span></span>
<span data-ttu-id="08cdd-124">Теперь вы можете использовать команды отладки в интегрированной среде сценариев для пошагового выполнения сценария ресурса, просмотра значений переменных, просмотра стека вызовов и т. д.</span><span class="sxs-lookup"><span data-stu-id="08cdd-124">Now you can use the debug commands in the ISE to step through the resource script, look at variable values, view the call stack, and so on.</span></span> <span data-ttu-id="08cdd-125">Помните, что каждая строка в сценарии ресурса (или классе) устанавливается в качестве точки останова.</span><span class="sxs-lookup"><span data-stu-id="08cdd-125">Remember that every line in the resource script (or class) is set as a break point.</span></span>

## <a name="disabling-dsc-debugging"></a><span data-ttu-id="08cdd-126">Отключение отладки DSC</span><span class="sxs-lookup"><span data-stu-id="08cdd-126">Disabling DSC debugging</span></span>

<span data-ttu-id="08cdd-127">После вызова командлета [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug) все вызовы [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) приведут к запуску отладчика для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="08cdd-127">After calling [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug), all calls to [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) will result in the configuration breaking into the debugger.</span></span> <span data-ttu-id="08cdd-128">Чтобы обеспечить нормальную работу конфигураций, необходимо отключить отладку, вызвав командлет [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug).</span><span class="sxs-lookup"><span data-stu-id="08cdd-128">To allow configurations to run normally, you must disable debugging by calling the [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug) cmdlet.</span></span>

><span data-ttu-id="08cdd-129">**Примечание**. Перезагрузка не меняет состояние отладки LCM.</span><span class="sxs-lookup"><span data-stu-id="08cdd-129">**Note:** Rebooting does not change the debug state of the LCM.</span></span> <span data-ttu-id="08cdd-130">Если отладка включена, после перезагрузки запуск конфигурации по-прежнему будет вызывать отладчик.</span><span class="sxs-lookup"><span data-stu-id="08cdd-130">If debugging is enabled, starting a configuration will still break into the debugger after a reboot.</span></span>

## <a name="see-also"></a><span data-ttu-id="08cdd-131">См. также</span><span class="sxs-lookup"><span data-stu-id="08cdd-131">See Also</span></span>

- [<span data-ttu-id="08cdd-132">Написание пользовательских ресурсов DSC с использованием MOF</span><span class="sxs-lookup"><span data-stu-id="08cdd-132">Writing a custom DSC resource with MOF</span></span>](../resources/authoringResourceMOF.md)
- [<span data-ttu-id="08cdd-133">Написание пользовательских ресурсов DSC с использованием классов PowerShell</span><span class="sxs-lookup"><span data-stu-id="08cdd-133">Writing a custom DSC resource with PowerShell classes</span></span>](../resources/authoringResourceClass.md)
