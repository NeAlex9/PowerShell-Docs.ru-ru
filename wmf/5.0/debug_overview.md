---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 9ead27fd5d4f146e9062488c1c8cc22a073b922e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187108"
---
# <a name="improvements-in-powershell-script-debugging"></a><span data-ttu-id="3b0e7-102">Усовершенствования отладки сценариев PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b0e7-102">Improvements in PowerShell Script Debugging</span></span>

<span data-ttu-id="3b0e7-103">В PowerShell 5.0 было внесено несколько усовершенствований, направленных на улучшение процедуры отладки.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-103">A number of improvements were made in PowerShell 5.0 to enhance the debugging experience:</span></span>

## <a name="break-all"></a><span data-ttu-id="3b0e7-104">Команда "Прервать все"</span><span class="sxs-lookup"><span data-stu-id="3b0e7-104">Break All</span></span>

<span data-ttu-id="3b0e7-105">Консоль PowerShell и интегрированная среда сценариев Windows PowerShell теперь позволяют переходить в режим отладчика при выполнении сценариев.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-105">The PowerShell console and Windows PowerShell ISE now allow you to break into the debugger for running scripts.</span></span> <span data-ttu-id="3b0e7-106">Это работает как в локальных, так и в удаленных сеансах.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-106">This works in both local and remote sessions.</span></span>

<span data-ttu-id="3b0e7-107">В окне консоли нажмите клавиши **CTRL+BREAK**.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-107">In the console, press **Ctrl+Break**.</span></span>

<span data-ttu-id="3b0e7-108">В интегрированной среде сценариев нажмите клавиши **CTRL+B** или воспользуйтесь командой меню **Отладка -> Прервать все**.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-108">In ISE, press **Ctrl+B**, or use the **Debug -> Break All** menu command.</span></span>

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a><span data-ttu-id="3b0e7-109">Удаленная отладка и удаленное редактирование файлов в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b0e7-109">Remote debugging and remote file editing in Windows PowerShell ISE</span></span>

<span data-ttu-id="3b0e7-110">Теперь среда Windows PowerShell позволяет открывать и редактировать файлы в удаленном сеансе, выполнив команду PSEdit.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-110">Windows PowerShell ISE now lets you open and edit files in a remote session by running the PSEdit command.</span></span>
<span data-ttu-id="3b0e7-111">Например, во время удаленного сеанса можно открыть файл для редактирования из командной строки, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3b0e7-111">For example, you can open a file for editing from the command line in a remote session as follows:</span></span>

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

<span data-ttu-id="3b0e7-112">Кроме того, можно вносить изменения и сохранять их в удаленном файле, который автоматически открывается в среде Windows PowerShell при попадании в точку останова.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-112">In addition, you can now edit and save changes in a remote file that is automatically opened in Windows PowerShell ISE when you hit a breakpoint.</span></span>
<span data-ttu-id="3b0e7-113">Теперь можно выполнить отладку файла сценария, выполняемого на удаленном компьютере, отредактировать файл, чтобы исправить ошибку, а затем снова запустить обновленный сценарий.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-113">Now, you can debug a script file that is running on a remote computer, edit the file to fix an error, and then rerun the modified script.</span></span>

## <a name="advanced-script-debugging"></a><span data-ttu-id="3b0e7-114">Расширенная отладка сценариев</span><span class="sxs-lookup"><span data-stu-id="3b0e7-114">Advanced Script Debugging</span></span>

<span data-ttu-id="3b0e7-115">Появились новые расширенные функции отладки, которые позволяют подключиться к любому процессу локального компьютера, загруженному в Windows PowerShell, и осуществить отладку произвольных пространств выполнения в нем.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-115">There are new, advanced debugging features that let you attach to any local computer process that has loaded Windows PowerShell, and debug arbitrary runspaces in that process.</span></span>

### <a name="runspace-debugging"></a><span data-ttu-id="3b0e7-116">Отладка пространств выполнения</span><span class="sxs-lookup"><span data-stu-id="3b0e7-116">Runspace Debugging</span></span>

<span data-ttu-id="3b0e7-117">Были добавлены новые командлеты, позволяющие вывести список текущих пространств выполнения в процессе, а также подключить консоль Windows PowerShell или отладчик интегрированной среды сценариев к такому пространству для отладки сценариев:</span><span class="sxs-lookup"><span data-stu-id="3b0e7-117">New cmdlets have been added that let you list current runspaces in a process, and attach the Windows PowerShell console or ISE debugger to that runspace for script debugging:</span></span>

-   <span data-ttu-id="3b0e7-118">Get-Runspace</span><span class="sxs-lookup"><span data-stu-id="3b0e7-118">Get-Runspace</span></span>
-   <span data-ttu-id="3b0e7-119">Debug-Runspace</span><span class="sxs-lookup"><span data-stu-id="3b0e7-119">Debug-Runspace</span></span>
-   <span data-ttu-id="3b0e7-120">Enable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="3b0e7-120">Enable-RunspaceDebug</span></span>
-   <span data-ttu-id="3b0e7-121">Disable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="3b0e7-121">Disable-RunspaceDebug</span></span>
-   <span data-ttu-id="3b0e7-122">Get-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="3b0e7-122">Get-RunspaceDebug</span></span>

### <a name="attach-to-process-hosting-powershell"></a><span data-ttu-id="3b0e7-123">Подключение к процессу, в котором размещается PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b0e7-123">Attach to Process hosting PowerShell</span></span>

<span data-ttu-id="3b0e7-124">Теперь вы можете подключиться к любому процессу на компьютере компьютера, в котором загружен Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b0e7-124">You can now attach to any computer process that has Windows PowerShell loaded.</span></span> <span data-ttu-id="3b0e7-125">Это можно сделать, перейдя в интерактивный сеанс с процессом, по аналогии со входом в интерактивный удаленный сеанс с помощью командлета Enter-PSSession:</span><span class="sxs-lookup"><span data-stu-id="3b0e7-125">You do this by entering into an interactive session with the process, similarly to how you enter into an interactive remote session by running the Enter-PSSession cmdlet:</span></span>

-   <span data-ttu-id="3b0e7-126">Enter-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="3b0e7-126">Enter-PSHostProcess</span></span>
-   <span data-ttu-id="3b0e7-127">Exit-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="3b0e7-127">Exit-PSHostProcess</span></span>
