---
title: Однострочные элементы кода и конвейеры
description: Однострочный элемент кода PowerShell — это один непрерывный конвейер, содержащий несколько команд, который позволяет выполнять одну задачу.
ms.date: 06/02/2020
ms.topic: guide
ms.custom: Contributor-mikefrobbins
ms.reviewer: mirobb
ms.openlocfilehash: b8fd45e5e5dc408754ebac015757ef4241428978
ms.sourcegitcommit: 109f132360e8adbbdaf5dbc42a270be73d9dfa9b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2020
ms.locfileid: "84633351"
---
# <a name="chapter-4---one-liners-and-the-pipeline"></a><span data-ttu-id="4e622-103">Глава 4. Однострочные элементы кода и конвейеры</span><span class="sxs-lookup"><span data-stu-id="4e622-103">Chapter 4 - One-liners and the pipeline</span></span>

<span data-ttu-id="4e622-104">На начальном этапе изучения PowerShell, если мне не удавалось выполнить задачу с помощью PowerShell, я возвращался к графическому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="4e622-104">When I first started learning PowerShell, if I couldn't accomplish a task with a PowerShell one-liner, I went back to the GUI.</span></span> <span data-ttu-id="4e622-105">Со временем я создал собственные техники написания сценариев, функций и модулей.</span><span class="sxs-lookup"><span data-stu-id="4e622-105">Over time, I built my skills up to writing scripts, functions, and modules.</span></span> <span data-ttu-id="4e622-106">Не пытайтесь углубляться в изучение сложных примеров, которые можно увидеть в Интернете.</span><span class="sxs-lookup"><span data-stu-id="4e622-106">Don't allow yourself to become overwhelmed by some of the more advanced examples you may see on the internet.</span></span> <span data-ttu-id="4e622-107">Сразу экспертами PowerShell не становятся.</span><span class="sxs-lookup"><span data-stu-id="4e622-107">No one is a natural expert with PowerShell.</span></span> <span data-ttu-id="4e622-108">Все мы когда-то были начинающими пользователями.</span><span class="sxs-lookup"><span data-stu-id="4e622-108">We were all beginners at one time.</span></span>

<span data-ttu-id="4e622-109">Тем из вас, кто еще использует графический интерфейс для администрирования, я советую установить средства управления на рабочей станции администратора и управлять серверами удаленно.</span><span class="sxs-lookup"><span data-stu-id="4e622-109">I have a bit of advice to offer those of you who are still using the GUI for administration: install the management tools on your admin workstation and manage your servers remotely.</span></span> <span data-ttu-id="4e622-110">В этом случае не важно, работает ли на сервере графический интерфейс пользователя или установка основных серверных компонентов операционной системы.</span><span class="sxs-lookup"><span data-stu-id="4e622-110">This way it won't matter if the server is running a GUI or Server Core installation of the operating system.</span></span>
<span data-ttu-id="4e622-111">Это поможет вам подготовиться к удаленному управлению серверами с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e622-111">It's going to help prepare you for managing servers remotely with PowerShell.</span></span>

<span data-ttu-id="4e622-112">Как говорилось и в предыдущих главах, обязательно следуйте инструкциям на компьютере с Windows 10 в лабораторной среде.</span><span class="sxs-lookup"><span data-stu-id="4e622-112">As with previous chapters, be sure to follow along on your Windows 10 lab environment computer.</span></span>

## <a name="one-liners"></a><span data-ttu-id="4e622-113">Однострочные элементы кода</span><span class="sxs-lookup"><span data-stu-id="4e622-113">One-Liners</span></span>

<span data-ttu-id="4e622-114">Однострочный элемент кода PowerShell — это один непрерывный конвейер, а не обязательно команда, которая приведена на одной физической строке.</span><span class="sxs-lookup"><span data-stu-id="4e622-114">A PowerShell one-liner is one continuous pipeline and not necessarily a command that’s on one physical line.</span></span> <span data-ttu-id="4e622-115">Не все команды, приведенные на одной физической строке, являются однострочным элементом кода.</span><span class="sxs-lookup"><span data-stu-id="4e622-115">Not all commands that are on one physical line are one-liners.</span></span>

<span data-ttu-id="4e622-116">Несмотря на то что следующая команда приведена на нескольких физических строках, она считается однострочным элементом кода PowerShell, потому что является одним непрерывным конвейером.</span><span class="sxs-lookup"><span data-stu-id="4e622-116">Even though the following command is on multiple physical lines, it's a PowerShell one-liner because it's one continuous pipeline.</span></span> <span data-ttu-id="4e622-117">Ее можно было записать на одной физической строке, но я выбрал разрыв строки рядом с вертикальной чертой.</span><span class="sxs-lookup"><span data-stu-id="4e622-117">It could be written on one physical line, but I've chosen to line break at the pipe symbol.</span></span> <span data-ttu-id="4e622-118">Вертикальная черта — один из символов, в котором допускается использовать естественный разрыв строки в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e622-118">The pipe symbol is one of the characters where a natural line break is allowed in PowerShell.</span></span>

```powershell
Get-Service |
  Where-Object CanPauseAndContinue -eq $true |
    Select-Object -Property *
```

```Output
Name                : LanmanWorkstation
RequiredServices    : {NSI, MRxSmb20, Bowser}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Workstation
DependentServices   : {SessionEnv, Netlogon, Browser}
MachineName         : .
ServiceName         : LanmanWorkstation
ServicesDependedOn  : {NSI, MRxSmb20, Bowser}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Automatic
Site                :
Container           :

Name                : Netlogon
RequiredServices    : {LanmanWorkstation}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Netlogon
DependentServices   : {}
MachineName         : .
ServiceName         : Netlogon
ServicesDependedOn  : {LanmanWorkstation}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Automatic
Site                :
Container           :

Name                : vmicheartbeat
RequiredServices    : {}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Hyper-V Heartbeat Service
DependentServices   : {}
MachineName         : .
ServiceName         : vmicheartbeat
ServicesDependedOn  : {}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :

Name                : vmickvpexchange
RequiredServices    : {}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Hyper-V Data Exchange Service
DependentServices   : {}
MachineName         : .
ServiceName         : vmickvpexchange
ServicesDependedOn  : {}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :

Name                : vmicrdv
RequiredServices    : {}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Hyper-V Remote Desktop Virtualization Service
DependentServices   : {}
MachineName         : .
ServiceName         : vmicrdv
ServicesDependedOn  : {}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :

Name                : vmicshutdown
RequiredServices    : {}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Hyper-V Guest Shutdown Service
DependentServices   : {}
MachineName         : .
ServiceName         : vmicshutdown
ServicesDependedOn  : {}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :

Name                : vmictimesync
RequiredServices    : {VmGid}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Hyper-V Time Synchronization Service
DependentServices   : {}
MachineName         : .
ServiceName         : vmictimesync
ServicesDependedOn  : {VmGid}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :

Name                : vmicvss
RequiredServices    : {}
CanPauseAndContinue : True
CanShutdown         : False
CanStop             : True
DisplayName         : Hyper-V Volume Shadow Copy Requestor
DependentServices   : {}
MachineName         : .
ServiceName         : vmicvss
ServicesDependedOn  : {}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :

Name                : Winmgmt
RequiredServices    : {RPCSS}
CanPauseAndContinue : True
CanShutdown         : True
CanStop             : True
DisplayName         : Windows Management Instrumentation
DependentServices   : {wscsvc, NcaSvc, iphlpsvc}
MachineName         : .
ServiceName         : Winmgmt
ServicesDependedOn  : {RPCSS}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Automatic
Site                :
Container           :
```

<span data-ttu-id="4e622-119">Естественные разрывы строк могут встречаться в часто используемых символах, включая запятую (`,`) и открывающие квадратные скобки (`[`), фигурные скобки (`{`) и круглые скобки (`(`).</span><span class="sxs-lookup"><span data-stu-id="4e622-119">Natural line breaks can occur at commonly used characters including comma (`,`) and opening brackets (`[`), braces (`{`), and parenthesis (`(`).</span></span> <span data-ttu-id="4e622-120">К другим, менее распространенным символам, относятся точка с запятой (`;`), знак равенства (`=`), а также открывающие одинарные и двойные кавычки (`'`, `"`).</span><span class="sxs-lookup"><span data-stu-id="4e622-120">Others that aren't so common include the semicolon (`;`), equals sign (`=`), and both opening single and double quotes (`'`,`"`).</span></span>

<span data-ttu-id="4e622-121">Использование обратной галочки (`` ` ``) или знака ударения в качестве символа продолжения строки является спорным.</span><span class="sxs-lookup"><span data-stu-id="4e622-121">Using the backtick (`` ` ``) or grave accent character as a line continuation character is a controversial topic.</span></span> <span data-ttu-id="4e622-122">Я советую стараться не использовать эти символы, если это вообще возможно.</span><span class="sxs-lookup"><span data-stu-id="4e622-122">My recommendation is to try to avoid it if at all possible.</span></span> <span data-ttu-id="4e622-123">Часто мне встречаются команды PowerShell, написанные с помощью обратной галочки, сразу за естественным символом разрыва строки.</span><span class="sxs-lookup"><span data-stu-id="4e622-123">I often see PowerShell commands written using a backtick immediately after a natural line break character.</span></span>
<span data-ttu-id="4e622-124">Она там абсолютна не нужна.</span><span class="sxs-lookup"><span data-stu-id="4e622-124">There's no reason for it to be there.</span></span>

```powershell
Get-Service -Name w32time |
>> Select-Object -Property *
```

```Output
Name                : w32time
RequiredServices    : {}
CanPauseAndContinue : False
CanShutdown         : True
CanStop             : True
DisplayName         : Windows Time
DependentServices   : {}
MachineName         : .
ServiceName         : w32time
ServicesDependedOn  : {}
ServiceHandle       : SafeServiceHandle
Status              : Running
ServiceType         : Win32ShareProcess
StartType           : Manual
Site                :
Container           :
```

<span data-ttu-id="4e622-125">Команды, показанные в предыдущих двух примерах, стабильно работают в консоли PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e622-125">The commands shown in the previous two examples work fine in the PowerShell console.</span></span> <span data-ttu-id="4e622-126">Но если вы запустите их в области консоли интегрированной среды сценариев PowerShell, они создадут ошибку.</span><span class="sxs-lookup"><span data-stu-id="4e622-126">But if you try to run them in the console pane of the PowerShell ISE, they'll generate an error.</span></span> <span data-ttu-id="4e622-127">В области консоли интегрированной среды сценариев PowerShell не предполагается, что остальная часть команды будет включена на следующей строке, как в консоли PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e622-127">The console pane of the PowerShell ISE doesn't wait for the rest of the command to be entered on the next line like the PowerShell console does.</span></span> <span data-ttu-id="4e622-128">Чтобы избежать этой проблемы в области консоли интегрированной среды сценариев PowerShell, используйте сочетание клавиш <kbd>Shift</kbd>+<kbd>ВВОД</kbd> вместо только клавиши <kbd>ВВОД</kbd>, когда продолжаете писать команду в другой строке.</span><span class="sxs-lookup"><span data-stu-id="4e622-128">To avoid this problem in the console pane of the PowerShell ISE, use <kbd>Shift</kbd>+<kbd>Enter</kbd> instead of just pressing <kbd>Enter</kbd> when continuing a command on another line.</span></span>

<span data-ttu-id="4e622-129">Следующий пример не является однострочным элементом кода PowerShell, так как он не является одним непрерывным конвейером.</span><span class="sxs-lookup"><span data-stu-id="4e622-129">This next example isn't a PowerShell one-liner because it's not one continuous pipeline.</span></span> <span data-ttu-id="4e622-130">Это две отдельные команды в одной строке, разделенные точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="4e622-130">It's two separate commands on one line, separated by a semicolon.</span></span>

```powershell
$Service = 'w32time'; Get-Service -Name $Service
```

```powershell
Status   Name               DisplayName
------   ----               -----------
Running  w32time            Windows Time
```

<span data-ttu-id="4e622-131">Во многих языках программирования и сценариев необходимо использовать точку с запятой в конце каждой строки.</span><span class="sxs-lookup"><span data-stu-id="4e622-131">Many programming and scripting languages require a semicolon at the end of each line.</span></span> <span data-ttu-id="4e622-132">Хотя их можно использовать таким образом в PowerShell, мы не советуем это делать, потому что эти символы не нужны.</span><span class="sxs-lookup"><span data-stu-id="4e622-132">While they can be used that way in PowerShell, it's not recommended because they're not needed.</span></span>

## <a name="filtering-left"></a><span data-ttu-id="4e622-133">Фильтрация по левому краю</span><span class="sxs-lookup"><span data-stu-id="4e622-133">Filtering Left</span></span>

<span data-ttu-id="4e622-134">Результаты команд, приведенные в этой главе, отфильтрованы по подмножеству.</span><span class="sxs-lookup"><span data-stu-id="4e622-134">The results of the commands shown in this chapter have been filtered down to a subset.</span></span> <span data-ttu-id="4e622-135">Например, `Get-Service` использовался с параметром **Name** для фильтрации списка служб, которые были возвращены только службе времени Windows.</span><span class="sxs-lookup"><span data-stu-id="4e622-135">For example, `Get-Service` was used with the **Name** parameter to filter the list of services that were returned to only the Windows Time service.</span></span>

<span data-ttu-id="4e622-136">В конвейере всегда нужно как можно раньше отфильтровать результаты по параметрам поиска.</span><span class="sxs-lookup"><span data-stu-id="4e622-136">In the pipeline, you always want to filter the results down to what you're looking for as early as possible.</span></span> <span data-ttu-id="4e622-137">Это выполняется с помощью параметров в первой команде или той, которая расположена в крайнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="4e622-137">This is accomplished using parameters on the first command or, the one to the far left.</span></span>
<span data-ttu-id="4e622-138">Иногда этот способ называется _фильтрация слева_.</span><span class="sxs-lookup"><span data-stu-id="4e622-138">This is sometimes called _filtering left_.</span></span>

<span data-ttu-id="4e622-139">В следующем примере используется параметр **Name** `Get-Service` для немедленной фильтрации результатов только в службе времени Windows.</span><span class="sxs-lookup"><span data-stu-id="4e622-139">The following example uses the **Name** parameter of `Get-Service` to immediately filter the results to the Windows Time service only.</span></span>

```powershell
Get-Service -Name w32time
```

```Output
Status   Name               DisplayName
------   ----               -----------
Running  w32time            Windows Time
```

<span data-ttu-id="4e622-140">Нередко встречаются примеры, в которых команда передается `Where-Object` для выполнения фильтрации.</span><span class="sxs-lookup"><span data-stu-id="4e622-140">It's not uncommon to see examples where the command is piped to `Where-Object` to perform the filtering.</span></span>

```powershell
Get-Service | Where-Object Name -eq w32time
```

```Output
Status   Name               DisplayName
------   ----               -----------
Running  W32Time            Windows Time
```

<span data-ttu-id="4e622-141">В первом примере фильтрация выполняется в источнике и результаты возвращаются только для службы времени Windows.</span><span class="sxs-lookup"><span data-stu-id="4e622-141">The first example filters at the source and only returns the results for the Windows Time service.</span></span>
<span data-ttu-id="4e622-142">Во втором примере возвращаются все службы, а затем они передаются другой команде для выполнения фильтрации.</span><span class="sxs-lookup"><span data-stu-id="4e622-142">The second example returns all the services then pipes them to another command to perform the filtering.</span></span> <span data-ttu-id="4e622-143">Хотя это может быть не так важно в следующем примере, но представьте, что вы запрашиваете список пользователей Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4e622-143">While this may not seem like a big deal in this example, imagine if you were querying a list of Active Directory users.</span></span> <span data-ttu-id="4e622-144">Вы точно хотите вернуть данные для нескольких тысяч учетных записей пользователей из Active Directory только для передачи их в другую команду, которая фильтрует учетные записи в небольшом подмножестве?</span><span class="sxs-lookup"><span data-stu-id="4e622-144">Do you really want to return the information for many thousands of user accounts from Active Directory only to pipe them to another command that filters them down to a tiny subset?</span></span> <span data-ttu-id="4e622-145">Я советую всегда выполнять фильтрацию по левому краю, даже если это кажется неважным.</span><span class="sxs-lookup"><span data-stu-id="4e622-145">My recommendation is to always filter left even when it doesn't seem to matter.</span></span> <span data-ttu-id="4e622-146">Вы привыкнете использовать этот способ и будете выполнять фильтрацию по левому краю автоматически, когда это действительно важно.</span><span class="sxs-lookup"><span data-stu-id="4e622-146">You'll be so use to it that you'll automatically filter left when it really does matter.</span></span>

<span data-ttu-id="4e622-147">Однажды мне кто-то сказал, что порядок, в котором указываются команды, не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="4e622-147">I once had someone tell me that the order you specify the commands in doesn't matter.</span></span> <span data-ttu-id="4e622-148">Это далеко от истины.</span><span class="sxs-lookup"><span data-stu-id="4e622-148">That couldn't be further from the truth.</span></span> <span data-ttu-id="4e622-149">Порядок, в котором указываются команды, действительно важен при выполнении фильтрации.</span><span class="sxs-lookup"><span data-stu-id="4e622-149">The order that the commands are specified in does indeed matter when performing filtering.</span></span> <span data-ttu-id="4e622-150">Например, рассмотрим ситуацию, при котором вы используете `Select-Object`, чтобы выбрать только несколько свойств, и `Where-Object` для фильтрации по свойствам, которые не будут находиться в выделенном фрагменте.</span><span class="sxs-lookup"><span data-stu-id="4e622-150">For example, consider the scenario where you are using `Select-Object` to select only a few properties and `Where-Object` to filter on properties that won't be in the selection.</span></span> <span data-ttu-id="4e622-151">В этом сценарии фильтрация должна выполняться первой, иначе свойство не будет существовать в конвейере при попытке выполнить фильтрацию.</span><span class="sxs-lookup"><span data-stu-id="4e622-151">In that scenario, the filtering must occur first, otherwise the property won't exist in the pipeline when try to perform the filtering.</span></span>

```powershell
Get-Service |
Select-Object -Property DisplayName, Running, Status |
Where-Object CanPauseAndContinue
```

<span data-ttu-id="4e622-152">Команда в предыдущем примере не возвращает результаты, так как свойство **CanStopAndContinue** не существует при передаче результатов из `Select-Object` в `Where-Object`.</span><span class="sxs-lookup"><span data-stu-id="4e622-152">The command in the previous example doesn't return any results because the **CanStopAndContinue** property doesn't exist when the results of `Select-Object` are piped to `Where-Object`.</span></span> <span data-ttu-id="4e622-153">Именно это свойство было "не выбрано".</span><span class="sxs-lookup"><span data-stu-id="4e622-153">That particular property wasn't "selected".</span></span> <span data-ttu-id="4e622-154">По сути, оно было отфильтровано. Обратная последовательность `Select-Object` и `Where-Object` выдает нужные результаты.</span><span class="sxs-lookup"><span data-stu-id="4e622-154">In essence, it was filtered out. Reversing the order of `Select-Object` and `Where-Object` produces the desired results.</span></span>

```powershell
Get-Service |
Where-Object CanPauseAndContinue |
Select-Object -Property DisplayName, Status
```

```Output
DisplayName                                    Status
-----------                                    ------
Workstation                                    Running
Netlogon                                       Running
Hyper-V Heartbeat Service                      Running
Hyper-V Data Exchange Service                  Running
Hyper-V Remote Desktop Virtualization Service  Running
Hyper-V Guest Shutdown Service                 Running
Hyper-V Time Synchronization Service           Running
Hyper-V Volume Shadow Copy Requestor           Running
Windows Management Instrumentation             Running
```

## <a name="the-pipeline"></a><span data-ttu-id="4e622-155">Конвейер</span><span class="sxs-lookup"><span data-stu-id="4e622-155">The Pipeline</span></span>

<span data-ttu-id="4e622-156">Как вы уже видели во многих примерах, показанных до настоящего момента в этом пособии, выходные данные одной команды можно несколько раз использовать в качестве входных данных для другой команды.</span><span class="sxs-lookup"><span data-stu-id="4e622-156">As you've seen in many of the examples shown so far throughout this book, many times the output of one command can be used as input for another command.</span></span> <span data-ttu-id="4e622-157">В главе 3 `Get-Member` использовался для определения типа объекта, который создает команда.</span><span class="sxs-lookup"><span data-stu-id="4e622-157">In Chapter 3, `Get-Member` was used to determine what type of object a command produces.</span></span> <span data-ttu-id="4e622-158">Кроме того, в этой же главе показано использование параметра **ParameterType** для `Get-Command`, которое позволяет определить команды, принявшие этот тип входных данных, хотя это необязательно выполняется входными данными конвейера.</span><span class="sxs-lookup"><span data-stu-id="4e622-158">Chapter 3 also showed using the **ParameterType** parameter of `Get-Command` to determine what commands accepted that type of input, although not necessarily by pipeline input.</span></span>

<span data-ttu-id="4e622-159">В зависимости от того, насколько полезна команда, она может включать раздел **INPUTS** и **OUTPUTS**.</span><span class="sxs-lookup"><span data-stu-id="4e622-159">Depending on how thorough a commands help is, it may include an **INPUTS** and **OUTPUTS** section.</span></span>

```powershell
help Stop-Service -Full
```

```Output
...
INPUTS
    System.ServiceProcess.ServiceController, System.String
        You can pipe a service object or a string that contains the name of a service
        to this cmdlet.

OUTPUTS
    None, System.ServiceProcess.ServiceController
        This cmdlet generates a System.ServiceProcess.ServiceController object that
        represents the service, if you use the PassThru parameter. Otherwise, this
        cmdlet does not generate any output.
...
```

<span data-ttu-id="4e622-160">В предыдущих результатах отображается только соответствующий раздел справки.</span><span class="sxs-lookup"><span data-stu-id="4e622-160">Only the relevant section of the help is shown in the previous results.</span></span> <span data-ttu-id="4e622-161">Как вы видите, в разделе **INPUTS** указано, что объект **ServiceController** или **String** может передаваться командлету `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-161">As you can see, the **INPUTS** section states that a **ServiceController** or a **String** object can be piped to the `Stop-Service` cmdlet.</span></span> <span data-ttu-id="4e622-162">Объект не сообщает, какие параметры принимают этот тип входных данных.</span><span class="sxs-lookup"><span data-stu-id="4e622-162">It doesn't tell you which parameters accept that type of input.</span></span> <span data-ttu-id="4e622-163">Проще всего определить эти данные при просмотре разных параметров в полной версии справки для командлета `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-163">One of the easiest ways to determine that information is to look through the different parameters in the full version of the help for the `Stop-Service` cmdlet.</span></span>

```powershell
help Stop-Service -Full
```

```powershell
...
-DisplayName <String[]>
    Specifies the display names of the services to stop. Wildcard characters are
    permitted.

    Required?                    true
    Position?                    named
    Default value                None
    Accept pipeline input?       False
    Accept wildcard characters?  false

-InputObject <ServiceController[]>
    Specifies ServiceController objects that represent the services to stop. Enter a
    variable that contains the objects, or type a command or expression that gets the
    objects.

    Required?                    true
    Position?                    0
    Default value                None
    Accept pipeline input?       True (ByValue)
    Accept wildcard characters?  false

-Name <String[]>
    Specifies the service names of the services to stop. Wildcard characters are
    permitted.

    Required?                    true
    Position?                    0
    Default value                None
    Accept pipeline input?       True (ByPropertyName, ByValue)
    Accept wildcard characters?  false
...
```

<span data-ttu-id="4e622-164">Еще раз замечу, что в предыдущем наборе результатов я показал только соответствующую часть справки.</span><span class="sxs-lookup"><span data-stu-id="4e622-164">Once again, I've only shown the relevant portion of the help in the previous set of results.</span></span> <span data-ttu-id="4e622-165">Обратите внимание, что параметр **DisplayName** не принимает входные данные конвейера, параметр **InputObject** принимает входные данные конвейера **по значению** для объектов **ServiceController**, а параметр **Name** принимает входные данные конвейера **по значению** для объектов **строки**.</span><span class="sxs-lookup"><span data-stu-id="4e622-165">Notice that the **DisplayName** parameter doesn't accept pipeline input, the **InputObject** parameter accepts pipeline input **by value** for **ServiceController** objects, and the **Name** parameter accepts pipeline input **by value** for **string** objects.</span></span> <span data-ttu-id="4e622-166">Кроме того, он принимает входные данные конвейера **по имени свойства**.</span><span class="sxs-lookup"><span data-stu-id="4e622-166">It also accepts pipeline input **by property name**.</span></span>

<span data-ttu-id="4e622-167">Если параметр принимает входные данные конвейера как по имени свойства, так и по значению, он всегда пытается сначала принять их **по значению**.</span><span class="sxs-lookup"><span data-stu-id="4e622-167">When a parameter accepts pipeline input by both property name and by value, it always tries **by value** first.</span></span> <span data-ttu-id="4e622-168">Если параметру не удается принять данные **по значению**, он пытается принять их **по имени свойства**.</span><span class="sxs-lookup"><span data-stu-id="4e622-168">If **by value** fails, then it tries **by property name**.</span></span> <span data-ttu-id="4e622-169">Вариант **по значению** не совсем точный.</span><span class="sxs-lookup"><span data-stu-id="4e622-169">**By value** is a little misleading.</span></span> <span data-ttu-id="4e622-170">Я предпочитаю называть его **по типу**.</span><span class="sxs-lookup"><span data-stu-id="4e622-170">I prefer to call it **by type**.</span></span> <span data-ttu-id="4e622-171">Это означает, что, если вы передаете результаты команды, которая создает тип объекта **ServiceController** для `Stop-Service`, он привязывает эти входные данные к параметру **InputObject**.</span><span class="sxs-lookup"><span data-stu-id="4e622-171">This means if you pipe the results of a command that produces a **ServiceController** object type to `Stop-Service`, it binds that input to the **InputObject** parameter.</span></span> <span data-ttu-id="4e622-172">Но если вы передаете результаты команды, которая создает выходные данные **String** в `Stop-Service`, объект привязывает их к параметру **Name**.</span><span class="sxs-lookup"><span data-stu-id="4e622-172">But if you pipe the results of a command that produces **String** output to `Stop-Service`, it binds it to the **Name** parameter.</span></span> <span data-ttu-id="4e622-173">Если вы передаете результаты команды, которая не создает объект **ServiceController** или **String** для `Stop-Service`, но при этом создает выходные данные, содержащие свойство с именем **Name**, объект привязывает свойство **Name** из выходных данных к параметру **Name** для `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-173">If you pipe the results of a command that doesn't produce a **ServiceController** or **String** object to `Stop-Service`, but it does produce output containing a property called **Name**, then it binds the **Name** property from the output to the **Name** parameter of `Stop-Service`.</span></span>

<span data-ttu-id="4e622-174">Определите, какой тип выходных данных создает команда `Get-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-174">Determine what type of output the `Get-Service` command produces.</span></span>

```powershell
Get-Service -Name w32time | Get-Member
```

```Output
   TypeName: System.ServiceProcess.ServiceController
```

<span data-ttu-id="4e622-175">`Get-Service` создает тип объекта ServiceController.</span><span class="sxs-lookup"><span data-stu-id="4e622-175">`Get-Service` produces a ServiceController object type.</span></span>

<span data-ttu-id="4e622-176">Как вы уже видели в справке, параметр **InputObject** для `Stop-Service` принимает объекты **ServiceController** через конвейер **по значению** (по типу).</span><span class="sxs-lookup"><span data-stu-id="4e622-176">As you previously saw in the help, the **InputObject** parameter of `Stop-Service` accepts **ServiceController** objects via the pipeline **by value** (by type).</span></span> <span data-ttu-id="4e622-177">Это означает, что, когда результаты командлета `Get-Service` передаются в `Stop-Service`, они привязываются к параметру **InputObject** для `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-177">This means that when the results of the `Get-Service` cmdlet are piped to `Stop-Service`, they bind to the **InputObject** parameter of `Stop-Service`.</span></span>

```powershell
Get-Service -Name w32time | Stop-Service
```

<span data-ttu-id="4e622-178">Теперь можно попробовать ввести строку.</span><span class="sxs-lookup"><span data-stu-id="4e622-178">Now to try string input.</span></span> <span data-ttu-id="4e622-179">Передайте `w32time` в `Get-Member`, только чтобы подтвердить, что это строка.</span><span class="sxs-lookup"><span data-stu-id="4e622-179">Pipe `w32time` to `Get-Member` just to confirm that it's a string.</span></span>

```powershell
'w32time' | Get-Member
```

```Output
   TypeName: System.String
```

<span data-ttu-id="4e622-180">Как уже было показано в справке, передача строки в `Stop-Service` привязывает ее **по значению** к параметру **Name** для `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-180">As previously shown in the help, piping a string to `Stop-Service` binds it **by value** to the **Name** parameter of `Stop-Service`.</span></span> <span data-ttu-id="4e622-181">Проверьте это, передав `w32time` в `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-181">Test this by piping `w32time` to `Stop-Service`.</span></span>

```powershell
'w32time' | Stop-Service
```

<span data-ttu-id="4e622-182">Заметьте, что в предыдущем примере я использовал одинарные кавычки вокруг строки `w32time`.</span><span class="sxs-lookup"><span data-stu-id="4e622-182">Notice that in the previous example, I used single quotes around the string `w32time`.</span></span> <span data-ttu-id="4e622-183">В PowerShell вы должны всегда использовать одинарные кавычки вместо двойных, если только содержимое строки в кавычках не содержит переменную, которая должна быть расширена до фактического значения.</span><span class="sxs-lookup"><span data-stu-id="4e622-183">In PowerShell, you should always use single quotes instead of double quotes unless the contents of the quoted string contains a variable that needs to be expanded to its actual value.</span></span> <span data-ttu-id="4e622-184">С помощью одинарных кавычек средству PowerShell не нужно анализировать содержимое, содержащееся в кавычках, поэтому ваш код будет выполняться быстрее.</span><span class="sxs-lookup"><span data-stu-id="4e622-184">By using single quotes, PowerShell doesn't have to parse the contents contained within the quotes so your code runs a little faster.</span></span>

<span data-ttu-id="4e622-185">Создайте пользовательский объект для проверки входных данных конвейера по имени свойства для параметра **Name** в `Stop-Service`.</span><span class="sxs-lookup"><span data-stu-id="4e622-185">Create a custom object to test pipeline input by property name for the **Name** parameter of `Stop-Service`.</span></span>

```powershell
$CustomObject = [pscustomobject]@{
 Name = 'w32time'
 }
```

<span data-ttu-id="4e622-186">Содержимое переменной **CustomObject** является типом объекта **PSCustomObject** и содержит свойство с именем **Name**.</span><span class="sxs-lookup"><span data-stu-id="4e622-186">The contents of the **CustomObject** variable is a **PSCustomObject** object type and it contains a property named **Name**.</span></span>

```powershell
$CustomObject | Get-Member
```

```Output
   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       bool Equals(System.Object obj)
GetHashCode Method       int GetHashCode()
GetType     Method       type GetType()
ToString    Method       string ToString()
Name        NoteProperty string Name=w32time
```

<span data-ttu-id="4e622-187">Если бы вы должны были заключить переменную `$CustomObject` в кавычки, вам бы пришлось использовать двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="4e622-187">If you were to surround the `$CustomObject` variable with quotes, you want to use double quotes.</span></span>
<span data-ttu-id="4e622-188">В противном случае при использовании одинарных кавычек строковый литерал `$CustomObject` передается в `Get-Member` вместо значения, содержащегося в переменной.</span><span class="sxs-lookup"><span data-stu-id="4e622-188">Otherwise, using single quotes, the literal string `$CustomObject` is piped to `Get-Member` instead of the value contained by the variable.</span></span>

<span data-ttu-id="4e622-189">Хотя передача содержимого `$CustomObject` в командлет `Stop-Service` привязывается к параметру **Name**, на этот раз он привязывается **по имени свойства**, а не **по значению**, так как содержимое `$CustomObject` является объектом, содержащим свойство с именем **Name**.</span><span class="sxs-lookup"><span data-stu-id="4e622-189">Although piping the contents of `$CustomObject` to `Stop-Service` cmdlet binds to the **Name** parameter, this time it binds **by property name** instead of **by value** because the contents of `$CustomObject` is an object that has a property named **Name**.</span></span>

<span data-ttu-id="4e622-190">В этом примере я создаю другой пользовательский объект, используя другое имя свойства, например **Service**.</span><span class="sxs-lookup"><span data-stu-id="4e622-190">In this example, I create another custom object using a different property name, such as **Service**.</span></span>

```powershell
$CustomObject = [pscustomobject]@{
  Service = 'w32time'
}
```

<span data-ttu-id="4e622-191">При попытке передать `$CustomObject` в `Stop-Service` создается ошибка, так как она не создает объект **ServiceController** или **String** и не содержит свойства с именем **Name**.</span><span class="sxs-lookup"><span data-stu-id="4e622-191">An error is generated when trying to pipe `$CustomObject` to `Stop-Service` because it doesn't produce a **ServiceController** or **String** object, and it doesn't have a property named **Name**.</span></span>

```powershell
$CustomObject | Stop-Service
```

```Output
Stop-Service : Cannot find any service with service name '@{Service=w32time}'.
At line:1 char:17
+ $CustomObject | Stop-Service
+
    + CategoryInfo          : ObjectNotFound: (@{Service=w32time}:String) [Stop-Service]
   , ServiceCommandException
    + FullyQualifiedErrorId : NoServiceFoundForGivenName,Microsoft.PowerShell.Commands.S
   topServiceCommand
```

<span data-ttu-id="4e622-192">Если выходные данные одной команды не выводятся с входными параметрами конвейера для другой команды, `Select-Object` можно использовать для переименования свойства таким образом, чтобы свойства были заданы правильно.</span><span class="sxs-lookup"><span data-stu-id="4e622-192">If the output of one command doesn't line up with the pipeline input options for another command, `Select-Object` can be used to rename the property so that the properties lineup correctly.</span></span>

```powershell
$CustomObject |
  Select-Object -Property @{name='Name';expression={$_.Service}} |
    Stop-Service
```

<span data-ttu-id="4e622-193">В этом примере `Select-Object` использовался для переименования свойства **Service** в свойство с именем **Name**.</span><span class="sxs-lookup"><span data-stu-id="4e622-193">In this example, `Select-Object` was used to rename the **Service** property to a property named **Name**.</span></span>

<span data-ttu-id="4e622-194">Синтаксис этого примера может сначала показаться немного сложным.</span><span class="sxs-lookup"><span data-stu-id="4e622-194">The syntax this example may seem a little complicated at first.</span></span> <span data-ttu-id="4e622-195">Единственное, что я понял: вы никогда не узнаете о синтаксисе, копируя и вставляя код.</span><span class="sxs-lookup"><span data-stu-id="4e622-195">What I have learned is that you'll never learn the syntax by copy and pasting code.</span></span> <span data-ttu-id="4e622-196">Потратьте время и несколько раз подряд введите код вручную.</span><span class="sxs-lookup"><span data-stu-id="4e622-196">Take the time to type the code in.</span></span> <span data-ttu-id="4e622-197">Потом это станет для вас привычным действием.</span><span class="sxs-lookup"><span data-stu-id="4e622-197">After a few times, it becomes second nature.</span></span> <span data-ttu-id="4e622-198">Наличие нескольких мониторов — большое преимущество, так как вы можете отобразить пример кода на одном экране и вводить его на другом.</span><span class="sxs-lookup"><span data-stu-id="4e622-198">Having multiple monitors is a huge benefit because you can display the example code on one screen and type it in on another one.</span></span>

<span data-ttu-id="4e622-199">Иногда вам придется использовать параметр, который не принимает входные данные конвейера.</span><span class="sxs-lookup"><span data-stu-id="4e622-199">Occasionally, you may want to use a parameter that doesn't accept pipeline input.</span></span> <span data-ttu-id="4e622-200">В следующем примере показано использование выходных данных одной команды в качестве входных данных для другой.</span><span class="sxs-lookup"><span data-stu-id="4e622-200">The following example demonstrates using the output of one command as input for another.</span></span> <span data-ttu-id="4e622-201">Сначала сохраните отображаемое имя для нескольких служб Windows в текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="4e622-201">First save the display name for a couple of Windows services into a text file.</span></span>

```powershell
'Background Intelligent Transfer Service', 'Windows Time' |
Out-File -FilePath $env:TEMP\services.txt
```

<span data-ttu-id="4e622-202">Вы можете выполнить команду, которая предоставляет необходимые выходные данные в круглых скобках в качестве значения параметра команды, требующей входные данные.</span><span class="sxs-lookup"><span data-stu-id="4e622-202">You can run the command that provides the needed output within parentheses as the value for the parameter of the command requiring the input.</span></span>

```powershell
Stop-Service -DisplayName (Get-Content -Path $env:TEMP\services.txt)
```

<span data-ttu-id="4e622-203">Это напоминает порядок операций в алгебре для тех, кто помнит, как это выглядит.</span><span class="sxs-lookup"><span data-stu-id="4e622-203">This is just like order of operations in Algebra for those of you who remember how it works.</span></span> <span data-ttu-id="4e622-204">Команда в круглых скобках всегда выполняется до внешней части команды.</span><span class="sxs-lookup"><span data-stu-id="4e622-204">The command within parentheses always runs prior to the outer portion of the command.</span></span>

## <a name="powershellget"></a><span data-ttu-id="4e622-205">PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="4e622-205">PowerShellGet</span></span>

<span data-ttu-id="4e622-206">PowerShellGet — это модуль PowerShell, который содержит команды для обнаружения, установки, публикации и обновления модулей PowerShell (и других артефактов) в репозиторий NuGet или из него.</span><span class="sxs-lookup"><span data-stu-id="4e622-206">PowerShellGet is a PowerShell module that contains commands for discovering, installing, publishing, and updating PowerShell modules (and other artifacts) to or from a NuGet repository.</span></span> <span data-ttu-id="4e622-207">PowerShellGet поставляется с PowerShell версии 5.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="4e622-207">PowerShellGet ships with PowerShell version 5.0 and higher.</span></span> <span data-ttu-id="4e622-208">Он доступен в виде отдельного скачиваемого файла для PowerShell версии 3.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="4e622-208">It is available as a separate download for PowerShell version 3.0 and higher.</span></span>

<span data-ttu-id="4e622-209">Корпорация Майкрософт размещает в Интернете репозиторий NuGet, который называется [Коллекция PowerShell][].</span><span class="sxs-lookup"><span data-stu-id="4e622-209">Microsoft hosts an online NuGet repository called the [PowerShell Gallery][].</span></span> <span data-ttu-id="4e622-210">Хотя этот репозиторий размещается Майкрософт, большинство модулей, которые в нем содержатся, пишутся не корпорацией.</span><span class="sxs-lookup"><span data-stu-id="4e622-210">Although this repository is hosted by Microsoft, the majority of the modules contained within the repository aren't written by Microsoft.</span></span> <span data-ttu-id="4e622-211">Любой код, полученный из коллекции PowerShell, необходимо тщательно проверить в изолированной тестовой среде, прежде чем считать его подходящим для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4e622-211">Any code obtain from the PowerShell Gallery should be thoroughly reviewed in an isolated test environment before being considered suitable for use in a production environment.</span></span>

<span data-ttu-id="4e622-212">Многим компаниям понадобится разместить собственный внутренний репозиторий NuGet, где они могут публиковать только внутренние модули, а также модули, загруженные ими из других источников, после того как они проверят, что эти модули не являются вредоносными.</span><span class="sxs-lookup"><span data-stu-id="4e622-212">Most companies will want to host their own internal private NuGet repository where they can post their internal use only modules as well as modules that they've downloaded from other sources once they've validated them as being non-malicious.</span></span>

<span data-ttu-id="4e622-213">Используйте командлет `Find-Module`, входящий в состав модуля PowerShellGet, чтобы найти модуль в коллекции PowerShell, который я написал, с именем MrToolkit.</span><span class="sxs-lookup"><span data-stu-id="4e622-213">Use the `Find-Module` cmdlet that's part of the PowerShellGet module to find a module in the PowerShell Gallery that I wrote named MrToolkit.</span></span>

```powershell
Find-Module -Name MrToolkit
```

```Output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with
NuGet-based repositories. The NuGet provider must be available in 'C:\Program
Files\PackageManagement\ProviderAssemblies' or
'C:\Users\MrAdmin\AppData\Local\PackageManagement\ProviderAssemblies'. You can also
install the NuGet provider by running 'Install-PackageProvider -Name NuGet
-MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the
NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.1        MrToolkit                           PSGallery            Misc PowerShell Tools
```

<span data-ttu-id="4e622-214">При первом использовании одной из команд из модуля PowerShellGet вам будет предложено установить поставщик NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e622-214">The first time you use one of the commands from the PowerShellGet module, you'll be prompted to install the NuGet provider.</span></span>

<span data-ttu-id="4e622-215">Чтобы установить модуль MrToolkit, передайте предыдущую команду в `Install-Module`.</span><span class="sxs-lookup"><span data-stu-id="4e622-215">To install the MrToolkit module, pipe the previous command to `Install-Module`.</span></span>

```powershell
Find-Module -Name MrToolkit | Install-Module
```

```Output
Untrusted repository
You are installing the modules from an untrusted repository. If you trust this
repository, change its InstallationPolicy value by running the Set-PSRepository cmdlet.
Are you sure you want to install the modules from
'https://www.powershellgallery.com/api/v2/'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): y
```

<span data-ttu-id="4e622-216">Так как коллекция PowerShell является недоверенным репозиторием, она предложит вам подтвердить установку модуля.</span><span class="sxs-lookup"><span data-stu-id="4e622-216">Since the PowerShell Gallery is an untrusted repository, it prompts you to approve the installation of the module.</span></span>

## <a name="finding-pipeline-input-the-easy-way"></a><span data-ttu-id="4e622-217">Простой способ поиска входных данных конвейера</span><span class="sxs-lookup"><span data-stu-id="4e622-217">Finding pipeline input the easy way</span></span>

<span data-ttu-id="4e622-218">Модуль MrToolkit содержит функцию с именем `Get-MrPipelineInput`.</span><span class="sxs-lookup"><span data-stu-id="4e622-218">The MrToolkit module contains a function named `Get-MrPipelineInput`.</span></span> <span data-ttu-id="4e622-219">С помощью этого командлета можно легко определить, какие параметры команды принимают входные данные конвейера, какой тип объекта они принимают, принимают ли они входные данные конвейера **по значению** или **по имени свойства**.</span><span class="sxs-lookup"><span data-stu-id="4e622-219">This cmdlet can be used to easily determine which parameters of a command accept pipeline input, what type of object they accept, and if they accept pipeline input **by value** or **by property name**.</span></span>

```powershell
Get-MrPipelineInput -Name Stop-Service
```

```Output
ParameterName ParameterType                             ValueFromPipeline ValueFromPipelineByPropertyName
------------- -------------                             ----------------- ---------------
InputObject   System.ServiceProcess.ServiceController[]              True           False
Name          System.String[]                                        True            True
```

<span data-ttu-id="4e622-220">Как видите, одни и те же данные, которые мы раньше определяли путем фильтрации справки, можно легко определять с помощью этой функции.</span><span class="sxs-lookup"><span data-stu-id="4e622-220">As you can see, the same information we previously determined by sifting through the help can easily be determined with this function.</span></span>

## <a name="summary"></a><span data-ttu-id="4e622-221">Сводка</span><span class="sxs-lookup"><span data-stu-id="4e622-221">Summary</span></span>

<span data-ttu-id="4e622-222">В этой главе вы узнали об однострочных элементах кода PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e622-222">In this chapter, you've learned about PowerShell one-liners.</span></span> <span data-ttu-id="4e622-223">Вы узнали, что количество физических строк, на которых приводится команда, не связано с однострочным элементом кода PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e622-223">You've learned that the number of physical lines that a command is on has nothing to do with whether or not it's a PowerShell one-liner.</span></span> <span data-ttu-id="4e622-224">Кроме того, вы получили представление о фильтрации по левому краю, конвейере и модуле PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="4e622-224">You've also learned about filtering left, the pipeline, and PowerShellGet.</span></span>

## <a name="review"></a><span data-ttu-id="4e622-225">Просмотр</span><span class="sxs-lookup"><span data-stu-id="4e622-225">Review</span></span>

1. <span data-ttu-id="4e622-226">Что такое однострочный элемент кода PowerShell?</span><span class="sxs-lookup"><span data-stu-id="4e622-226">What is a PowerShell one-liner?</span></span>
1. <span data-ttu-id="4e622-227">В каких нескольких символах допускаются естественные разрывы строк в PowerShell?</span><span class="sxs-lookup"><span data-stu-id="4e622-227">What are some of the characters where natural line breaks can occur in PowerShell?</span></span>
1. <span data-ttu-id="4e622-228">Зачем выполнять фильтрацию по левому краю?</span><span class="sxs-lookup"><span data-stu-id="4e622-228">Why should you filter left?</span></span>
1. <span data-ttu-id="4e622-229">С помощью каких двух способов команда PowerShell может принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4e622-229">What are the two ways that a PowerShell command can accept pipeline input?</span></span>
1. <span data-ttu-id="4e622-230">Почему не следует доверять командам, найденным в коллекции PowerShell?</span><span class="sxs-lookup"><span data-stu-id="4e622-230">Why shouldn't you trust commands found in the PowerShell Gallery?</span></span>

## <a name="recommended-reading"></a><span data-ttu-id="4e622-231">Рекомендуем прочесть</span><span class="sxs-lookup"><span data-stu-id="4e622-231">Recommended Reading</span></span>

- <span data-ttu-id="4e622-232">[about_Pipelines][]</span><span class="sxs-lookup"><span data-stu-id="4e622-232">[about_Pipelines][]</span></span>
- <span data-ttu-id="4e622-233">[about_Command_Syntax][]</span><span class="sxs-lookup"><span data-stu-id="4e622-233">[about_Command_Syntax][]</span></span>
- <span data-ttu-id="4e622-234">[about_Parameters][]</span><span class="sxs-lookup"><span data-stu-id="4e622-234">[about_Parameters][]</span></span>
- <span data-ttu-id="4e622-235">[PowerShellGet: ПРОСТОЙ, НО ВАЖНЫЙ способ обнаружения, установки и обновления модулей PowerShell][psget]</span><span class="sxs-lookup"><span data-stu-id="4e622-235">[PowerShellGet: The BIG EASY way to discover, install, and update PowerShell modules][psget]</span></span>

<!-- link references-->
[about_Pipelines]: /powershell/module/microsoft.powershell.core/about/about_pipelines
[about_Command_Syntax]: /powershell/module/microsoft.powershell.core/about/about_command_syntax
[about_Parameters]: /powershell/module/microsoft.powershell.core/about/about_parameters
[psget]: https://mikefrobbins.com/2015/04/23/powershellget-the-big-easy-way-to-discover-install-and-update-powershell-modules/
[Коллекция PowerShell]: https://www.powershellgallery.com/
[PowerShell Gallery]: https://www.powershellgallery.com/
