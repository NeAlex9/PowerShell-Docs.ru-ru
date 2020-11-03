---
description: Описание запуска и записи скриптов в PowerShell.
keywords: powershell,командлет
Locale: en-US
ms.date: 10/06/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Scripts
ms.openlocfilehash: 9b82f5c24397036e4560d3c8f84e7e403769c207
ms.sourcegitcommit: f874dc1d4236e06a3df195d179f59e0a7d9f8436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "93231254"
---
# <a name="about-scripts"></a><span data-ttu-id="5ccf1-104">О скриптах</span><span class="sxs-lookup"><span data-stu-id="5ccf1-104">About Scripts</span></span>

## <a name="short-description"></a><span data-ttu-id="5ccf1-105">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="5ccf1-105">Short description</span></span>
<span data-ttu-id="5ccf1-106">Описание запуска и записи скриптов в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-106">Describes how to run and write scripts in PowerShell.</span></span>

## <a name="long-description"></a><span data-ttu-id="5ccf1-107">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="5ccf1-107">Long description</span></span>

<span data-ttu-id="5ccf1-108">Сценарий — это обычный текстовый файл, содержащий одну или несколько команд PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-108">A script is a plain text file that contains one or more PowerShell commands.</span></span>
<span data-ttu-id="5ccf1-109">Сценарии PowerShell имеют `.ps1` расширение файла.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-109">PowerShell scripts have a `.ps1` file extension.</span></span>

<span data-ttu-id="5ccf1-110">Выполнение сценария во многом похоже на выполнение командлета.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-110">Running a script is a lot like running a cmdlet.</span></span> <span data-ttu-id="5ccf1-111">Введите путь и имя файла скрипта и используйте параметры для отправки данных и задания параметров.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-111">You type the path and file name of the script and use parameters to submit data and set options.</span></span> <span data-ttu-id="5ccf1-112">Сценарии можно запускать на компьютере или в удаленном сеансе на другом компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-112">You can run scripts on your computer or in a remote session on a different computer.</span></span>

<span data-ttu-id="5ccf1-113">Написание сценария сохраняет команду для последующего использования и упрощает совместное использование с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-113">Writing a script saves a command for later use and makes it easy to share with others.</span></span> <span data-ttu-id="5ccf1-114">Что самое важное, это позволяет выполнять команды просто путем ввода пути скрипта и имени файла.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-114">Most importantly, it lets you run the commands simply by typing the script path and the filename.</span></span> <span data-ttu-id="5ccf1-115">Скрипты могут быть простыми как одной командой в файле, так и сложной программой.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-115">Scripts can be as simple as a single command in a file or as extensive as a complex program.</span></span>

<span data-ttu-id="5ccf1-116">Сценарии имеют дополнительные функции, такие как `#Requires` Специальный комментарий, использование параметров, поддержка разделов данных и цифровая подпись для обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-116">Scripts have additional features, such as the `#Requires` special comment, the use of parameters, support for data sections, and digital signing for security.</span></span>
<span data-ttu-id="5ccf1-117">Также можно написать разделы справки для скриптов и для любых функций в скрипте.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-117">You can also write Help topics for scripts and for any functions in the script.</span></span>

## <a name="how-to-run-a-script"></a><span data-ttu-id="5ccf1-118">Выполнение сценария</span><span class="sxs-lookup"><span data-stu-id="5ccf1-118">How to run a script</span></span>

<span data-ttu-id="5ccf1-119">Прежде чем можно будет запустить сценарий в Windows, необходимо изменить политику выполнения PowerShell по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-119">Before you can run a script on Windows, you need to change the default PowerShell execution policy.</span></span> <span data-ttu-id="5ccf1-120">Политика выполнения не применяется к PowerShell, работающему на платформах, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-120">Execution policy does not apply to PowerShell running on non-Windows platforms.</span></span>

<span data-ttu-id="5ccf1-121">Политика выполнения по умолчанию `Restricted` предотвращает выполнение всех скриптов, включая скрипты, которые вы пишете на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-121">The default execution policy, `Restricted`, prevents all scripts from running, including scripts that you write on the local computer.</span></span> <span data-ttu-id="5ccf1-122">Подробнее см. в разделе [about_Execution_Policies](about_Execution_Policies.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-122">For more information, see [about_Execution_Policies](about_Execution_Policies.md).</span></span>

<span data-ttu-id="5ccf1-123">Политика выполнения сохраняется в реестре, поэтому ее необходимо изменить только один раз на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-123">The execution policy is saved in the registry, so you need to change it only once on each computer.</span></span>

<span data-ttu-id="5ccf1-124">Чтобы изменить политику выполнения, используйте следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-124">To change the execution policy, use the following procedure.</span></span>

<span data-ttu-id="5ccf1-125">В командной строке введите:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-125">At the command prompt, type:</span></span>

```powershell
Set-ExecutionPolicy AllSigned
```

<span data-ttu-id="5ccf1-126">or</span><span class="sxs-lookup"><span data-stu-id="5ccf1-126">or</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<span data-ttu-id="5ccf1-127">Изменение вступает в силу немедленно.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-127">The change is effective immediately.</span></span>

<span data-ttu-id="5ccf1-128">Чтобы выполнить сценарий, введите полное имя файла скрипта и полный путь к нему.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-128">To run a script, type the full name and the full path to the script file.</span></span>

<span data-ttu-id="5ccf1-129">Например, чтобы запустить сценарий Get-ServiceLog.ps1 в каталоге C:\Scripts, введите:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-129">For example, to run the Get-ServiceLog.ps1 script in the C:\Scripts directory, type:</span></span>

```powershell
C:\Scripts\Get-ServiceLog.ps1
```

<span data-ttu-id="5ccf1-130">Чтобы выполнить сценарий в текущем каталоге, введите путь к текущему каталогу или используйте точку для представления текущего каталога, после чего следует обратная косая черта ( `.\` ).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-130">To run a script in the current directory, type the path to the current directory, or use a dot to represent the current directory, followed by a path backslash (`.\`).</span></span>

<span data-ttu-id="5ccf1-131">Например, чтобы запустить сценарий ServicesLog.ps1 в локальном каталоге, введите:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-131">For example, to run the ServicesLog.ps1 script in the local directory, type:</span></span>

```powershell
.\Get-ServiceLog.ps1
```

<span data-ttu-id="5ccf1-132">Если у скрипта есть параметры, введите параметры и значения параметров после имени файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-132">If the script has parameters, type the parameters and parameter values after the script filename.</span></span>

<span data-ttu-id="5ccf1-133">Например, следующая команда использует параметр ServiceName скрипта Get-ServiceLog, чтобы запросить журнал действия службы удаленного управления Windows.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-133">For example, the following command uses the ServiceName parameter of the Get-ServiceLog script to request a log of WinRM service activity.</span></span>

```powershell
.\Get-ServiceLog.ps1 -ServiceName WinRM
```

<span data-ttu-id="5ccf1-134">В качестве функции безопасности PowerShell не выполняет сценарии при двойном щелчке значка скрипта в проводнике или при вводе имени сценария без полного пути, даже если сценарий находится в текущем каталоге.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-134">As a security feature, PowerShell does not run scripts when you double-click the script icon in File Explorer or when you type the script name without a full path, even when the script is in the current directory.</span></span> <span data-ttu-id="5ccf1-135">Дополнительные сведения о выполнении команд и сценариев в PowerShell см. в разделе [about_Command_Precedence](about_Command_Precedence.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-135">For more information about running commands and scripts in PowerShell, see [about_Command_Precedence](about_Command_Precedence.md).</span></span>

### <a name="run-with-powershell"></a><span data-ttu-id="5ccf1-136">Запуск с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ccf1-136">Run with PowerShell</span></span>

<span data-ttu-id="5ccf1-137">Начиная с PowerShell 3,0 можно запускать сценарии из проводника.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-137">Beginning in PowerShell 3.0, you can run scripts from File Explorer.</span></span>

<span data-ttu-id="5ccf1-138">Чтобы использовать функцию "Запуск с помощью PowerShell", сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-138">To use the "Run with PowerShell" feature:</span></span>

<span data-ttu-id="5ccf1-139">Запустите проводник, щелкните правой кнопкой мыши имя файла скрипта и выберите команду "запустить с помощью PowerShell".</span><span class="sxs-lookup"><span data-stu-id="5ccf1-139">Run File Explorer, right-click the script filename and then select "Run with PowerShell".</span></span>

<span data-ttu-id="5ccf1-140">Функция "запустить с помощью PowerShell" предназначена для выполнения скриптов, которые не имеют обязательных параметров и не возвращают выходные данные в командную строку.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-140">The "Run with PowerShell" feature is designed to run scripts that do not have required parameters and do not return output to the command prompt.</span></span>

<span data-ttu-id="5ccf1-141">Дополнительные сведения см. в разделе [about_Run_With_PowerShell](about_Run_With_PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-141">For more information, see [about_Run_With_PowerShell](about_Run_With_PowerShell.md).</span></span>

### <a name="running-scripts-on-other-computers"></a><span data-ttu-id="5ccf1-142">Выполнение сценариев на других компьютерах</span><span class="sxs-lookup"><span data-stu-id="5ccf1-142">Running scripts on other computers</span></span>

<span data-ttu-id="5ccf1-143">Чтобы запустить сценарий на одном или нескольких удаленных компьютерах, используйте параметр **FilePath** `Invoke-Command` командлета.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-143">To run a script on one or more remote computers, use the **FilePath** parameter of the `Invoke-Command` cmdlet.</span></span>

<span data-ttu-id="5ccf1-144">Введите путь и имя файла скрипта в качестве значения параметра **FilePath** .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-144">Enter the path and filename of the script as the value of the **FilePath** parameter.</span></span> <span data-ttu-id="5ccf1-145">Скрипт должен находиться на локальном компьютере или в каталоге, к которому локальный компьютер может получить доступ.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-145">The script must reside on the local computer or in a directory that the local computer can access.</span></span>

<span data-ttu-id="5ccf1-146">Следующая команда запускает `Get-ServiceLog.ps1` сценарий на удаленных компьютерах с именем Server01 и Server02.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-146">The following command runs the `Get-ServiceLog.ps1` script on the remote computers named Server01 and Server02.</span></span>

```powershell
Invoke-Command -ComputerName Server01,Server02 -FilePath `
  C:\Scripts\Get-ServiceLog.ps1
```

## <a name="get-help-for-scripts"></a><span data-ttu-id="5ccf1-147">Получить справку по сценариям</span><span class="sxs-lookup"><span data-stu-id="5ccf1-147">Get help for scripts</span></span>

<span data-ttu-id="5ccf1-148">Командлет Get-Help получает разделы справки для скриптов, а также для командлетов и других типов команд.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-148">The Get-Help cmdlet gets the help topics for scripts as well as for cmdlets and other types of commands.</span></span> <span data-ttu-id="5ccf1-149">Чтобы получить раздел справки для скрипта, введите, `Get-Help` за которым следует путь и имя файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-149">To get the help topic for a script, type `Get-Help` followed by the path and filename of the script.</span></span> <span data-ttu-id="5ccf1-150">Если путь к скрипту находится в `Path` переменной среды, путь можно опустить.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-150">If the script path is in your `Path` environment variable, you can omit the path.</span></span>

<span data-ttu-id="5ccf1-151">Например, чтобы получить справку по сценарию ServicesLog.ps1, введите:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-151">For example, to get help for the ServicesLog.ps1 script, type:</span></span>

```powershell
get-help C:\admin\scripts\ServicesLog.ps1
```

## <a name="how-to-write-a-script"></a><span data-ttu-id="5ccf1-152">Написание сценария</span><span class="sxs-lookup"><span data-stu-id="5ccf1-152">How to write a script</span></span>

<span data-ttu-id="5ccf1-153">Скрипт может содержать любые допустимые команды PowerShell, в том числе отдельные команды, команды, использующие конвейер, функции и управляющие структуры, такие как операторы If и циклы for.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-153">A script can contain any valid PowerShell commands, including single commands, commands that use the pipeline, functions, and control structures such as If statements and For loops.</span></span>

<span data-ttu-id="5ccf1-154">Чтобы написать сценарий, откройте новый файл в текстовом редакторе, введите команды и сохраните их в файле с допустимым именем файла с `.ps1` расширением.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-154">To write a script, open a new file in a text editor, type the commands, and save them in a file with a valid filename with the `.ps1` file extension.</span></span>

<span data-ttu-id="5ccf1-155">Следующий пример представляет собой простой сценарий, который получает службы, работающие в текущей системе, и сохраняет их в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-155">The following example is a simple script that gets the services that are running on the current system and saves them to a log file.</span></span> <span data-ttu-id="5ccf1-156">Имя файла журнала создается с текущей даты.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-156">The log filename is created from the current date.</span></span>

```powershell
$date = (get-date).dayofyear
get-service | out-file "$date.log"
```

<span data-ttu-id="5ccf1-157">Чтобы создать этот скрипт, откройте текстовый редактор или редактор скриптов, введите следующие команды, а затем сохраните их в файле с именем `ServiceLog.ps1` .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-157">To create this script, open a text editor or a script editor, type these commands, and then save them in a file named `ServiceLog.ps1`.</span></span>

### <a name="parameters-in-scripts"></a><span data-ttu-id="5ccf1-158">Параметры в скриптах</span><span class="sxs-lookup"><span data-stu-id="5ccf1-158">Parameters in scripts</span></span>

<span data-ttu-id="5ccf1-159">Чтобы определить параметры в скрипте, используйте инструкцию param.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-159">To define parameters in a script, use a Param statement.</span></span> <span data-ttu-id="5ccf1-160">`Param`Инструкция должна быть первой инструкцией в скрипте, за исключением комментариев и любых `#Require` инструкций.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-160">The `Param` statement must be the first statement in a script, except for comments and any `#Require` statements.</span></span>

<span data-ttu-id="5ccf1-161">Параметры сценария работают как параметры функции.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-161">Script parameters work like function parameters.</span></span> <span data-ttu-id="5ccf1-162">Значения параметров доступны для всех команд в скрипте.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-162">The parameter values are available to all of the commands in the script.</span></span> <span data-ttu-id="5ccf1-163">Все функции параметров функций, включая атрибут Parameter и его именованные аргументы, также допустимы в скриптах.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-163">All of the features of function parameters, including the Parameter attribute and its named arguments, are also valid in scripts.</span></span>

<span data-ttu-id="5ccf1-164">При выполнении скрипта пользователи заменяют параметры после имени скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-164">When running the script, script users type the parameters after the script name.</span></span>

<span data-ttu-id="5ccf1-165">В следующем примере показан `Test-Remote.ps1` скрипт с параметром **ComputerName** .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-165">The following example shows a `Test-Remote.ps1` script that has a **ComputerName** parameter.</span></span> <span data-ttu-id="5ccf1-166">Обе функции сценария могут обращаться к значению параметра **ComputerName** .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-166">Both of the script functions can access the **ComputerName** parameter value.</span></span>

```powershell
param ($ComputerName = $(throw "ComputerName parameter is required."))

function CanPing {
   $error.clear()
   $tmp = test-connection $computername -erroraction SilentlyContinue

   if (!$?)
       {write-host "Ping failed: $ComputerName."; return $false}
   else
       {write-host "Ping succeeded: $ComputerName"; return $true}
}

function CanRemote {
    $s = new-pssession $computername -erroraction SilentlyContinue

    if ($s -is [System.Management.Automation.Runspaces.PSSession])
        {write-host "Remote test succeeded: $ComputerName."}
    else
        {write-host "Remote test failed: $ComputerName."}
}

if (CanPing $computername) {CanRemote $computername}
```

<span data-ttu-id="5ccf1-167">Чтобы выполнить этот скрипт, введите имя параметра после имени скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-167">To run this script, type the parameter name after the script name.</span></span> <span data-ttu-id="5ccf1-168">Пример:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-168">For example:</span></span>

```powershell
C:\PS> .\test-remote.ps1 -computername Server01

Ping succeeded: Server01
Remote test failed: Server01
```

<span data-ttu-id="5ccf1-169">Дополнительные сведения о инструкции Param и параметрах функции см. в разделе [about_Functions](about_Functions.md) и [about_Functions_Advanced_Parameters](about_Functions_Advanced_Parameters.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-169">For more information about the Param statement and the function parameters, see [about_Functions](about_Functions.md) and [about_Functions_Advanced_Parameters](about_Functions_Advanced_Parameters.md).</span></span>

### <a name="writing-help-for-scripts"></a><span data-ttu-id="5ccf1-170">Написание справки для сценариев</span><span class="sxs-lookup"><span data-stu-id="5ccf1-170">Writing help for scripts</span></span>

<span data-ttu-id="5ccf1-171">Раздел справки для скрипта можно написать с помощью любого из двух следующих методов.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-171">You can write a help topic for a script by using either of the two following methods:</span></span>

- <span data-ttu-id="5ccf1-172">Comment-Based справки по сценариям</span><span class="sxs-lookup"><span data-stu-id="5ccf1-172">Comment-Based Help for Scripts</span></span>

  <span data-ttu-id="5ccf1-173">Создайте раздел справки, используя специальные ключевые слова в комментариях.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-173">Create a Help topic by using special keywords in the comments.</span></span> <span data-ttu-id="5ccf1-174">Чтобы создать справку на основе комментариев для сценария, необходимо поместить комментарии в начало или в конец файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-174">To create comment-based Help for a script, the comments must be placed at the beginning or end of the script file.</span></span> <span data-ttu-id="5ccf1-175">Дополнительные сведения о справке на основе комментариев см. в разделе [about_Comment_Based_Help](about_Comment_Based_Help.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-175">For more information about comment-based Help, see [about_Comment_Based_Help](about_Comment_Based_Help.md).</span></span>

- <span data-ttu-id="5ccf1-176">XML-Based справки по сценариям</span><span class="sxs-lookup"><span data-stu-id="5ccf1-176">XML-Based Help  for Scripts</span></span>

  <span data-ttu-id="5ccf1-177">Создайте раздел справки на основе XML, например тип, который обычно создается для командлетов.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-177">Create an XML-based Help topic, such as the type that is typically created for cmdlets.</span></span> <span data-ttu-id="5ccf1-178">При преобразовании разделов справки на несколько языков требуется справка на основе XML.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-178">XML-based Help is required if you are translating Help topics into multiple languages.</span></span>

<span data-ttu-id="5ccf1-179">Чтобы связать скрипт с разделом справки на основе XML, используйте. Ключевое слово комментария справки Екстерналхелп.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-179">To associate the script with the XML-based Help topic, use the .ExternalHelp Help comment keyword.</span></span> <span data-ttu-id="5ccf1-180">Дополнительные сведения о ключевом слове Екстерналхелп см. в разделе [about_Comment_Based_Help](about_Comment_Based_Help.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-180">For more information about the ExternalHelp keyword, see [about_Comment_Based_Help](about_Comment_Based_Help.md).</span></span> <span data-ttu-id="5ccf1-181">Дополнительные сведения о справке на основе XML см. [в разделе как написать справку по командлетам](/powershell/scripting/developer/help/writing-help-for-windows-powershell-cmdlets).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-181">For more information about XML-based help, see [How to Write Cmdlet Help](/powershell/scripting/developer/help/writing-help-for-windows-powershell-cmdlets).</span></span>

### <a name="returning-an-exit-value"></a><span data-ttu-id="5ccf1-182">Возврат значения выхода</span><span class="sxs-lookup"><span data-stu-id="5ccf1-182">Returning an exit value</span></span>

<span data-ttu-id="5ccf1-183">По умолчанию скрипты не возвращают состояние выхода при завершении сценария.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-183">By default, scripts do not return an exit status when the script ends.</span></span> <span data-ttu-id="5ccf1-184">`exit`Для возврата кода выхода из скрипта необходимо использовать инструкцию.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-184">You must use the `exit` statement to return an exit code from a script.</span></span> <span data-ttu-id="5ccf1-185">По умолчанию `exit` инструкция возвращает `0` .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-185">By default, the `exit` statement returns `0`.</span></span> <span data-ttu-id="5ccf1-186">Можно указать числовое значение, чтобы вернуть другое состояние выхода.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-186">You can provide a numeric value to return a different exit status.</span></span> <span data-ttu-id="5ccf1-187">Ненулевое значение кода выхода обычно сигнализирует об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-187">A nonzero exit code typically signals a failure.</span></span>

<span data-ttu-id="5ccf1-188">В Windows допускается любое число между `[int]::MinValue` и `[int]::MaxValue` .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-188">On Windows, any number between `[int]::MinValue` and `[int]::MaxValue` is allowed.</span></span>

<span data-ttu-id="5ccf1-189">В UNIX разрешены только положительные числа в диапазоне от `[byte]::MinValue` (0) до `[byte]::MaxValue` (255).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-189">On Unix, only positive numbers between `[byte]::MinValue` (0) and `[byte]::MaxValue` (255) are allowed.</span></span> <span data-ttu-id="5ccf1-190">Отрицательное число в диапазоне от `-1` до `-255` автоматически преобразуется в положительное число путем добавления</span><span class="sxs-lookup"><span data-stu-id="5ccf1-190">A negative number in the range of `-1` through `-255` is automatically translated into a positive number by adding</span></span>
256. <span data-ttu-id="5ccf1-191">Например, `-2` преобразуется в `254` .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-191">For example, `-2` is transformed to `254`.</span></span>

<span data-ttu-id="5ccf1-192">В PowerShell `exit` инструкция задает значение `$LASTEXITCODE` переменной.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-192">In PowerShell, the `exit` statement sets the value of the `$LASTEXITCODE` variable.</span></span> <span data-ttu-id="5ccf1-193">В командной оболочке Windows (cmd.exe) оператор Exit задает значение `%ERRORLEVEL%` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-193">In the Windows Command Shell (cmd.exe), the exit statement sets the value of the `%ERRORLEVEL%` environment variable.</span></span>

<span data-ttu-id="5ccf1-194">Любой аргумент, который не является числовым или вне диапазона, зависящего от платформы, преобразуется в значение `0` .</span><span class="sxs-lookup"><span data-stu-id="5ccf1-194">Any argument that is non-numeric or outside the platform-specific range is translated to the value of `0`.</span></span>

## <a name="script-scope-and-dot-sourcing"></a><span data-ttu-id="5ccf1-195">Область скрипта и источники с точкой</span><span class="sxs-lookup"><span data-stu-id="5ccf1-195">Script scope and dot sourcing</span></span>

<span data-ttu-id="5ccf1-196">Каждый скрипт выполняется в отдельной области.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-196">Each script runs in its own scope.</span></span> <span data-ttu-id="5ccf1-197">Функции, переменные, псевдонимы и диски, созданные в сценарии, существуют только в области скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-197">The functions, variables, aliases, and drives that are created in the script exist only in the script scope.</span></span> <span data-ttu-id="5ccf1-198">Доступ к этим элементам или их значениям в области, в которой выполняется скрипт, невозможен.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-198">You cannot access these items or their values in the scope in which the script runs.</span></span>

<span data-ttu-id="5ccf1-199">Чтобы выполнить скрипт в другой области, можно указать область, например Global или local, или создать точку для скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-199">To run a script in a different scope, you can specify a scope, such as Global or Local, or you can dot source the script.</span></span>

<span data-ttu-id="5ccf1-200">Функция «с точкой» позволяет запускать скрипт в текущей области, а не в области скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-200">The dot sourcing feature lets you run a script in the current scope instead of in the script scope.</span></span> <span data-ttu-id="5ccf1-201">При запуске скрипта, который имеет точку с точкой, команды в скрипте выполняются так, будто были введены в командной строке.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-201">When you run a script that is dot sourced, the commands in the script run as though you had typed them at the command prompt.</span></span> <span data-ttu-id="5ccf1-202">Функции, переменные, псевдонимы и диски, создаваемые сценарием, создаются в области, в которой выполняется работа.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-202">The functions, variables, aliases, and drives that the script creates are created in the scope in which you are working.</span></span> <span data-ttu-id="5ccf1-203">После выполнения скрипта можно использовать созданные элементы и получить доступ к их значениям в сеансе.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-203">After the script runs, you can use the created items and access their values in your session.</span></span>

<span data-ttu-id="5ccf1-204">Чтобы создать точку скрипта для исходного кода, введите точку (.) и пробел перед путем к сценарию.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-204">To dot source a script, type a dot (.) and a space before the script path.</span></span>

<span data-ttu-id="5ccf1-205">Пример:</span><span class="sxs-lookup"><span data-stu-id="5ccf1-205">For example:</span></span>

```powershell
. C:\scripts\UtilityFunctions.ps1
```

<span data-ttu-id="5ccf1-206">или диспетчер конфигурации служб</span><span class="sxs-lookup"><span data-stu-id="5ccf1-206">or</span></span>

```powershell
. .\UtilityFunctions.ps1
```

<span data-ttu-id="5ccf1-207">После `UtilityFunctions.ps1` выполнения скрипта функции и переменные, создаваемые сценарием, добавляются в текущую область.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-207">After the `UtilityFunctions.ps1` script runs, the functions and variables that the script creates are added to the current scope.</span></span>

<span data-ttu-id="5ccf1-208">Например, `UtilityFunctions.ps1` Скрипт создает `New-Profile` функцию и `$ProfileName` переменную.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-208">For example, the `UtilityFunctions.ps1` script creates the `New-Profile` function and the `$ProfileName` variable.</span></span>

```powershell
#In UtilityFunctions.ps1

function New-Profile
{
  Write-Host "Running New-Profile function"
  $profileName = split-path $profile -leaf

  if (test-path $profile)
    {write-error "Profile $profileName already exists on this computer."}
  else
    {new-item -type file -path $profile -force }
}
```

<span data-ttu-id="5ccf1-209">При запуске `UtilityFunctions.ps1` скрипта в собственной области скрипта `New-Profile` функция и `$ProfileName` переменная существуют только во время выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-209">If you run the `UtilityFunctions.ps1` script in its own script scope, the `New-Profile` function and the `$ProfileName` variable exist only while the script is running.</span></span> <span data-ttu-id="5ccf1-210">При завершении работы скрипта удаляется функция и переменная, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-210">When the script exits, the function and variable are removed, as shown in the following example.</span></span>

```powershell
C:\PS> .\UtilityFunctions.ps1

C:\PS> New-Profile
The term 'new-profile' is not recognized as a cmdlet, function, operable
program, or script file. Verify the term and try again.
At line:1 char:12
+ new-profile <<<<
   + CategoryInfo          : ObjectNotFound: (new-profile:String) [],
   + FullyQualifiedErrorId : CommandNotFoundException

C:\PS> $profileName
C:\PS>
```

<span data-ttu-id="5ccf1-211">Когда вы подаете скрипту точку и запускаете его, сценарий создает `New-Profile` функцию и `$ProfileName` переменную в своем сеансе в вашей области.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-211">When you dot source the script and run it, the script creates the `New-Profile` function and the `$ProfileName` variable in your session in your scope.</span></span> <span data-ttu-id="5ccf1-212">После выполнения скрипта можно использовать `New-Profile` функцию в сеансе, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-212">After the script runs, you can use the `New-Profile` function in your session, as shown in the following example.</span></span>

```powershell
C:\PS> . .\UtilityFunctions.ps1

C:\PS> New-Profile

    Directory: C:\Users\juneb\Documents\WindowsPowerShell

    Mode    LastWriteTime     Length Name
    ----    -------------     ------ ----
    -a---   1/14/2009 3:08 PM      0 Microsoft.PowerShellISE_profile.ps1

C:\PS> $profileName
Microsoft.PowerShellISE_profile.ps1
```

<span data-ttu-id="5ccf1-213">Дополнительные сведения об области действия см. в разделе about_Scopes.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-213">For more information about scope, see about_Scopes.</span></span>

## <a name="scripts-in-modules"></a><span data-ttu-id="5ccf1-214">Скрипты в модулях</span><span class="sxs-lookup"><span data-stu-id="5ccf1-214">Scripts in modules</span></span>

<span data-ttu-id="5ccf1-215">Модуль — это набор связанных ресурсов PowerShell, которые можно распространять как единое целое.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-215">A module is a set of related PowerShell resources that can be distributed as a unit.</span></span> <span data-ttu-id="5ccf1-216">Вы можете использовать модули для организации скриптов, функций и других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-216">You can use modules to organize your scripts, functions, and other resources.</span></span> <span data-ttu-id="5ccf1-217">Можно также использовать модули для распространения кода среди других пользователей и получения кода из надежных источников.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-217">You can also use modules to distribute your code to others, and to get code from trusted sources.</span></span>

<span data-ttu-id="5ccf1-218">Можно включить скрипты в модули или создать модуль скрипта, который представляет собой модуль, полностью или в основном содержащий скрипт и вспомогательные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-218">You can include scripts in your modules, or you can create a script module, which is a module that consists entirely or primarily of a script and supporting resources.</span></span> <span data-ttu-id="5ccf1-219">Модуль скрипта — это просто сценарий с расширением файла PSM1.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-219">A script module is just a script with a .psm1 file extension.</span></span>

<span data-ttu-id="5ccf1-220">Дополнительные сведения о модулях см. в разделе [about_Modules](about_Modules.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-220">For more information about modules, see [about_Modules](about_Modules.md).</span></span>

## <a name="other-script-features"></a><span data-ttu-id="5ccf1-221">Другие функции сценариев</span><span class="sxs-lookup"><span data-stu-id="5ccf1-221">Other script features</span></span>

<span data-ttu-id="5ccf1-222">В PowerShell есть много полезных функций, которые можно использовать в скриптах.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-222">PowerShell has many useful features that you can use in scripts.</span></span>

- <span data-ttu-id="5ccf1-223">`#Requires` — Можно использовать `#Requires` инструкцию, чтобы предотвратить выполнение скрипта без указанных модулей или оснасток и заданную версию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-223">`#Requires` - You can use a `#Requires` statement to prevent a script from running without specified modules or snap-ins and a specified version of PowerShell.</span></span> <span data-ttu-id="5ccf1-224">Дополнительные сведения см. в разделе about_Requires.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-224">For more information, see about_Requires.</span></span>

- <span data-ttu-id="5ccf1-225">`$PSCommandPath` — Содержит полный путь и имя выполняемого скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-225">`$PSCommandPath` - Contains the full path and name of the script that is being run.</span></span> <span data-ttu-id="5ccf1-226">Этот параметр допустим во всех скриптах.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-226">This parameter is valid in all scripts.</span></span> <span data-ttu-id="5ccf1-227">Эта автоматическая переменная появилась в PowerShell 3,0.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-227">This automatic variable is introduced in PowerShell 3.0.</span></span>

- <span data-ttu-id="5ccf1-228">`$PSScriptRoot` — Содержит каталог, из которого выполняется скрипт.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-228">`$PSScriptRoot` - Contains the directory from which a script is being run.</span></span> <span data-ttu-id="5ccf1-229">В PowerShell 2,0 эта переменная допустима только в модулях скриптов ( `.psm1` ).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-229">In PowerShell 2.0, this variable is valid only in script modules (`.psm1`).</span></span>
  <span data-ttu-id="5ccf1-230">Начиная с PowerShell 3,0, он действителен во всех скриптах.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-230">Beginning in PowerShell 3.0, it is valid in all scripts.</span></span>

- <span data-ttu-id="5ccf1-231">`$MyInvocation` — `$MyInvocation` Автоматическая переменная содержит сведения о текущем скрипте, включая сведения о том, как он был запущен или вызван.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-231">`$MyInvocation` - The `$MyInvocation` automatic variable contains information about the current script, including information about how it was started or "invoked."</span></span> <span data-ttu-id="5ccf1-232">Эту переменную и ее свойства можно использовать для получения сведений о скрипте во время его выполнения.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-232">You can use this variable and its properties to get information about the script while it is running.</span></span> <span data-ttu-id="5ccf1-233">Например, `$MyInvocation` . Переменная Микомманд. path содержит путь и имя файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-233">For example, the `$MyInvocation`.MyCommand.Path variable contains the path and filename of the script.</span></span> <span data-ttu-id="5ccf1-234">`$MyInvocation`. Строка содержит команду, которая запустила скрипт, включая все параметры и значения.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-234">`$MyInvocation`.Line contains the command that started the script, including all parameters and values.</span></span>

  <span data-ttu-id="5ccf1-235">Начиная с PowerShell 3,0, `$MyInvocation` имеет два новых свойства, которые предоставляют сведения о скрипте, который вызывал или вызывает текущий скрипт.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-235">Beginning in PowerShell 3.0, `$MyInvocation` has two new properties that provide information about the script that called or invoked the current script.</span></span> <span data-ttu-id="5ccf1-236">Значения этих свойств заполняются только в том случае, если вызывающий элемент или вызвавший объект является сценарием.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-236">The values of these properties are populated only when the invoker or caller is a script.</span></span>

  - <span data-ttu-id="5ccf1-237">**Пскоммандпас** содержит полный путь и имя скрипта, который вызывал или вызывает текущий скрипт.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-237">**PSCommandPath** contains the full path and name of the script that called or invoked the current script.</span></span>

  - <span data-ttu-id="5ccf1-238">**PSScriptRoot** содержит каталог скрипта, вызвавшего или вызвавшего текущий скрипт.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-238">**PSScriptRoot** contains the directory of the script that called or invoked the current script.</span></span>

  <span data-ttu-id="5ccf1-239">В отличие от `$PSCommandPath` и `$PSScriptRoot` автоматических переменных, содержащих сведения о текущем скрипте, свойства **пскоммандпас** и **PSScriptRoot** этой `$MyInvocation` переменной содержат сведения о скрипте, вызвавшем текущий скрипт.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-239">Unlike the `$PSCommandPath` and `$PSScriptRoot` automatic variables, which contain information about the current script, the **PSCommandPath** and **PSScriptRoot** properties of the `$MyInvocation` variable contain information about the script that called the current script.</span></span>

- <span data-ttu-id="5ccf1-240">Разделы данных. Вы можете использовать `Data` ключевое слово для разделения данных из логики в скриптах.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-240">Data sections - You can use the `Data` keyword to separate data from logic in scripts.</span></span> <span data-ttu-id="5ccf1-241">Разделы данных также могут упростить локализацию.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-241">Data sections can also make localization easier.</span></span> <span data-ttu-id="5ccf1-242">Дополнительные сведения см. в разделе [about_Data_Sections](about_Data_Sections.md) и [about_Script_Internationalization](about_Script_Internationalization.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-242">For more information, see [about_Data_Sections](about_Data_Sections.md) and [about_Script_Internationalization](about_Script_Internationalization.md).</span></span>

- <span data-ttu-id="5ccf1-243">Подпись скрипта. Вы можете добавить цифровую подпись к сценарию.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-243">Script Signing - You can add a digital signature to a script.</span></span> <span data-ttu-id="5ccf1-244">В зависимости от политики выполнения можно использовать цифровые подписи для ограничения выполнения скриптов, которые могут включать ненадежные команды.</span><span class="sxs-lookup"><span data-stu-id="5ccf1-244">Depending on the execution policy, you can use digital signatures to restrict the running of scripts that could include unsafe commands.</span></span> <span data-ttu-id="5ccf1-245">Дополнительные сведения см. в разделе [about_Execution_Policies](about_Execution_Policies.md) и [about_Signing](about_Signing.md).</span><span class="sxs-lookup"><span data-stu-id="5ccf1-245">For more information, see [about_Execution_Policies](about_Execution_Policies.md) and [about_Signing](about_Signing.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5ccf1-246">См. также статью</span><span class="sxs-lookup"><span data-stu-id="5ccf1-246">See also</span></span>

[<span data-ttu-id="5ccf1-247">about_Command_Precedence</span><span class="sxs-lookup"><span data-stu-id="5ccf1-247">about_Command_Precedence</span></span>](about_Command_Precedence.md)

[<span data-ttu-id="5ccf1-248">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="5ccf1-248">about_Comment_Based_Help</span></span>](about_Comment_Based_Help.md)

[<span data-ttu-id="5ccf1-249">about_Execution_Policies</span><span class="sxs-lookup"><span data-stu-id="5ccf1-249">about_Execution_Policies</span></span>](about_Execution_Policies.md)

[<span data-ttu-id="5ccf1-250">about_Functions</span><span class="sxs-lookup"><span data-stu-id="5ccf1-250">about_Functions</span></span>](about_Functions.md)

[<span data-ttu-id="5ccf1-251">about_Modules</span><span class="sxs-lookup"><span data-stu-id="5ccf1-251">about_Modules</span></span>](about_Modules.md)

[<span data-ttu-id="5ccf1-252">about_Profiles</span><span class="sxs-lookup"><span data-stu-id="5ccf1-252">about_Profiles</span></span>](about_Profiles.md)

[<span data-ttu-id="5ccf1-253">about_Requires</span><span class="sxs-lookup"><span data-stu-id="5ccf1-253">about_Requires</span></span>](about_Requires.md)

[<span data-ttu-id="5ccf1-254">about_Run_With_PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ccf1-254">about_Run_With_PowerShell</span></span>](about_Run_With_PowerShell.md)

[<span data-ttu-id="5ccf1-255">about_Scopes</span><span class="sxs-lookup"><span data-stu-id="5ccf1-255">about_Scopes</span></span>](about_Scopes.md)

[<span data-ttu-id="5ccf1-256">about_Script_Blocks</span><span class="sxs-lookup"><span data-stu-id="5ccf1-256">about_Script_Blocks</span></span>](about_Script_Blocks.md)

[<span data-ttu-id="5ccf1-257">about_Signing</span><span class="sxs-lookup"><span data-stu-id="5ccf1-257">about_Signing</span></span>](about_Signing.md)

[<span data-ttu-id="5ccf1-258">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="5ccf1-258">Invoke-Command</span></span>](xref:Microsoft.PowerShell.Core.Invoke-Command)
