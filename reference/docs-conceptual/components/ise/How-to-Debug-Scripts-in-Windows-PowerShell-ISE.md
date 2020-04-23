---
ms.date: 01/02/2020
keywords: powershell,командлет
title: Отладка сценариев в интегрированной среде сценариев Windows PowerShell
ms.openlocfilehash: 6fbe340cbff832b5d0e2a5515ef432cec574a3c1
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "80500941"
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="a5beb-103">Отладка сценариев в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5beb-103">How to Debug Scripts in Windows PowerShell ISE</span></span>

<span data-ttu-id="a5beb-104">В этой статье описано, как отлаживать сценарии на локальном компьютере визуальными инструментами отладки интегрированной среды сценариев (ISE) Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5beb-104">This article describes how to debug scripts on a local computer by using the Windows PowerShell Integrated Scripting Environment (ISE) visual debugging features.</span></span>

## <a name="how-to-manage-breakpoints"></a><span data-ttu-id="a5beb-105">Управление точками останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-105">How to manage breakpoints</span></span>

<span data-ttu-id="a5beb-106">Точка останова — это назначенная точка в сценарии, на которой выполнение временно останавливается, чтобы можно было проверить текущее состояние переменных и среды, в которой выполняется сценарий.</span><span class="sxs-lookup"><span data-stu-id="a5beb-106">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span>
<span data-ttu-id="a5beb-107">После приостановки сценария в точке останова можно выполнить команды в области консоли для проверки его состояния.</span><span class="sxs-lookup"><span data-stu-id="a5beb-107">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span> <span data-ttu-id="a5beb-108">Можно выводить переменные и выполнять другие команды.</span><span class="sxs-lookup"><span data-stu-id="a5beb-108">You can output variables or run other commands.</span></span> <span data-ttu-id="a5beb-109">Можно даже изменять значения любых переменных, видимых в контексте текущего выполняемого сценария.</span><span class="sxs-lookup"><span data-stu-id="a5beb-109">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="a5beb-110">После получения нужных сведений можно продолжить выполнение сценария.</span><span class="sxs-lookup"><span data-stu-id="a5beb-110">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="a5beb-111">В среде отладки Windows PowerShell можно установить три вида точек останова:</span><span class="sxs-lookup"><span data-stu-id="a5beb-111">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1. <span data-ttu-id="a5beb-112">**Точка останова по строке**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-112">**Line breakpoint**.</span></span> <span data-ttu-id="a5beb-113">Сценарий приостанавливается при достижении назначенной строки.</span><span class="sxs-lookup"><span data-stu-id="a5beb-113">The script pauses when the designated line is reached during the operation of the script</span></span>

1. <span data-ttu-id="a5beb-114">**Точка останова переменной.**</span><span class="sxs-lookup"><span data-stu-id="a5beb-114">**Variable breakpoint.**</span></span> <span data-ttu-id="a5beb-115">Сценарий приостанавливается при изменении значения, назначенного переменной.</span><span class="sxs-lookup"><span data-stu-id="a5beb-115">The script pauses whenever the designated variable's value changes.</span></span>

1. <span data-ttu-id="a5beb-116">**Точка останова команды.**</span><span class="sxs-lookup"><span data-stu-id="a5beb-116">**Command breakpoint.**</span></span> <span data-ttu-id="a5beb-117">Сценарий приостанавливается перед выполнением назначенной команды.</span><span class="sxs-lookup"><span data-stu-id="a5beb-117">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="a5beb-118">Можно указать параметры, чтобы отфильтровать для точки останова только нужную операцию.</span><span class="sxs-lookup"><span data-stu-id="a5beb-118">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="a5beb-119">Команда также может быть созданной вами функцией.</span><span class="sxs-lookup"><span data-stu-id="a5beb-119">The command can also be a function you created.</span></span>

<span data-ttu-id="a5beb-120">В среде отладки интегрированной среды сценариев Windows PowerShell только точки останова по строке можно задать с помощью меню или сочетаний клавиш.</span><span class="sxs-lookup"><span data-stu-id="a5beb-120">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="a5beb-121">Точки останова двух других типов также можно задать, но в области консоли, используя командлет [Set-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Set-PSBreakpoint).</span><span class="sxs-lookup"><span data-stu-id="a5beb-121">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Set-PSBreakpoint) cmdlet.</span></span> <span data-ttu-id="a5beb-122">В этом разделе описано, как выполнять задачи отладки в интегрированной среде сценариев Windows PowerShell, по возможности используя меню, и выполнять более широкий набор команд из области консоли, используя сценарии.</span><span class="sxs-lookup"><span data-stu-id="a5beb-122">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="a5beb-123">Задание точки останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-123">To set a breakpoint</span></span>

<span data-ttu-id="a5beb-124">Точку останова можно задать в сценарии только после его сохранения.</span><span class="sxs-lookup"><span data-stu-id="a5beb-124">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="a5beb-125">Щелкните правой кнопкой мыши строку, где нужно задать точку останова, и выберите пункт **Точка останова**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-125">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="a5beb-126">Другой вариант: щелкните строку, где нужно задать точку останова, и нажмите клавишу <kbd>F9</kbd> либо выберите **Точка останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-126">Or, click the line where you want to set a line breakpoint, and press <kbd>F9</kbd> or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="a5beb-127">Следующий сценарий — пример создания точки останова по переменной из области консоли с помощью командлета [Set-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Set-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-127">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Set-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="a5beb-128">Перечисление всех точек останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-128">List all breakpoints</span></span>

<span data-ttu-id="a5beb-129">Отображает все точки останова в текущем сеансе Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5beb-129">Displays all breakpoints in the current Windows PowerShell session.</span></span>

<span data-ttu-id="a5beb-130">В меню **Отладка** выберите пункт **Вывести список точек останова**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-130">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="a5beb-131">Следующий сценарий — пример перечисления всех точек останова из области консоли с помощью командлета [Get-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Get-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-131">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Get-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="a5beb-132">Удаление точки останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-132">Remove a breakpoint</span></span>

<span data-ttu-id="a5beb-133">Удаляет указанную точку останова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-133">Removing a breakpoint deletes it.</span></span>

<span data-ttu-id="a5beb-134">Если вы считаете, что точка останова может понадобиться в будущем, лучше [отключите](#disable-a-breakpoint) ее.</span><span class="sxs-lookup"><span data-stu-id="a5beb-134">If you think you might want to use it again later, consider [Disable a Breakpoint](#disable-a-breakpoint) it instead.</span></span> <span data-ttu-id="a5beb-135">Щелкните правой кнопкой мыши строку, где нужно удалить точку останова, и выберите пункт **ToggleBreakpoint** (Точка останова).</span><span class="sxs-lookup"><span data-stu-id="a5beb-135">Right-click the line where you want to remove a breakpoint, and then click **ToggleBreakpoint**.</span></span>
<span data-ttu-id="a5beb-136">Другой вариант: щелкните строку, где нужно удалить точку останова, и выберите пункт **Точка останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-136">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span> <span data-ttu-id="a5beb-137">Следующий сценарий — пример удаления точки останова с указанным идентификатором из области консоли с помощью командлета [Remove-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Remove-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-137">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Remove-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="a5beb-138">Удаление всех точек останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-138">Remove All Breakpoints</span></span>

<span data-ttu-id="a5beb-139">Чтобы удалить все точки останова, определенные в текущем сеансе, выберите команду **Удалить все точки останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-139">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="a5beb-140">Следующий сценарий — пример удаления всех точек останова из области консоли с помощью командлета [Remove-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Remove-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-140">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Remove-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a><span data-ttu-id="a5beb-141">Отключение точки останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-141">Disable a Breakpoint</span></span>

<span data-ttu-id="a5beb-142">Отключение точки не приводит к ее удалению; она просто остается неактивной, пока не будет включена.</span><span class="sxs-lookup"><span data-stu-id="a5beb-142">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span> <span data-ttu-id="a5beb-143">Щелкните правой кнопкой мыши строку, где нужно отключить точку останова, и выберите команду **Отключить точку останова**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-143">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="a5beb-144">Другой вариант: щелкните строку, где нужно отключить точку останова, и нажмите клавишу <kbd>F9</kbd> либо выберите **Отключить точку останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-144">Or, click the line where you want to disable a breakpoint, and press <kbd>F9</kbd> or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="a5beb-145">Следующий сценарий — пример отключения точки останова с указанным идентификатором из области консоли с помощью командлета [Disable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Disable-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-145">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Disable-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="a5beb-146">Отключение всех точек останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-146">Disable All Breakpoints</span></span>

<span data-ttu-id="a5beb-147">Отключение точки не приводит к ее удалению; она просто остается неактивной, пока не будет включена.</span><span class="sxs-lookup"><span data-stu-id="a5beb-147">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span> <span data-ttu-id="a5beb-148">Чтобы отключить все точки останова в текущем сеансе, выберите команду **Отключить все точки останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-148">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="a5beb-149">Следующий сценарий — пример отключения всех точек останова из области консоли с помощью командлета [Disable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Disable-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-149">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Disable-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="a5beb-150">Включение точки останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-150">Enable a Breakpoint</span></span>

<span data-ttu-id="a5beb-151">Щелкните правой кнопкой мыши строку, где нужно включить точку останова, и выберите команду **Включить точку останова**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-151">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="a5beb-152">Другой вариант: щелкните строку, где нужно включить точку останова, и нажмите клавишу <kbd>F9</kbd> либо выберите **Включить точку останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-152">Or, click the line where you want to enable a breakpoint, and then press <kbd>F9</kbd> or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="a5beb-153">Следующий сценарий — пример включения отдельных точек останова из области консоли с помощью командлета [Enable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Enable-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-153">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Enable-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="a5beb-154">Включение всех точек останова</span><span class="sxs-lookup"><span data-stu-id="a5beb-154">Enable All Breakpoints</span></span>

<span data-ttu-id="a5beb-155">Чтобы включить все точки останова, определенные в текущем сеансе, выберите команду **Включить все точки останова** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-155">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="a5beb-156">Следующий сценарий — пример включения всех точек останова из области консоли с помощью командлета [Enable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Enable-PSBreakpoint):</span><span class="sxs-lookup"><span data-stu-id="a5beb-156">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Enable-PSBreakpoint) cmdlet.</span></span>

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a><span data-ttu-id="a5beb-157">Управление сеансом отладки</span><span class="sxs-lookup"><span data-stu-id="a5beb-157">How to manage a debugging session</span></span>

<span data-ttu-id="a5beb-158">Перед запуском отладки нужно задать одну или несколько точек останова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-158">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="a5beb-159">Точки останова нельзя задавать, если отлаживаемый сценарий не сохранен.</span><span class="sxs-lookup"><span data-stu-id="a5beb-159">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="a5beb-160">Инструкции по заданию точек останова см. в статье [Управление точками останова](#how-to-manage-breakpoints) или [Set-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Set-PSBreakpoint).</span><span class="sxs-lookup"><span data-stu-id="a5beb-160">For directions on of how to set a breakpoint, see [How to manage breakpoints](#how-to-manage-breakpoints) or [Set-PSBreakpoint](/powershell/module/Microsoft.PowerShell.Utility/Set-PSBreakpoint).</span></span>
<span data-ttu-id="a5beb-161">После начала отладки сценарий нельзя редактировать до ее окончания.</span><span class="sxs-lookup"><span data-stu-id="a5beb-161">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="a5beb-162">Сценарий, содержащий одну или несколько точек останова, автоматически сохраняется перед запуском.</span><span class="sxs-lookup"><span data-stu-id="a5beb-162">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="a5beb-163">Начало отладки</span><span class="sxs-lookup"><span data-stu-id="a5beb-163">To start debugging</span></span>

<span data-ttu-id="a5beb-164">Нажмите клавишу <kbd>F5</kbd>, щелкните значок **Выполнить сценарий** на панели инструментов или выберите **Выполнить/продолжить** в меню **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="a5beb-164">Press <kbd>F5</kbd> or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="a5beb-165">Сценарий выполняется до первой точки останова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-165">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="a5beb-166">В ней он приостанавливается и выделяет соответствующую строку.</span><span class="sxs-lookup"><span data-stu-id="a5beb-166">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="a5beb-167">Продолжение отладки</span><span class="sxs-lookup"><span data-stu-id="a5beb-167">To continue debugging</span></span>

<span data-ttu-id="a5beb-168">Нажмите клавишу <kbd>F5</kbd>, щелкните значок **Run Script** (Выполнить сценарий) на панели инструментов, выберите **Run/Continue** (Выполнить/продолжить) в меню **Debug** (Отладка) либо введите `C` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-168">Press <kbd>F5</kbd> or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type `C` and then press <kbd>ENTER</kbd>.</span></span> <span data-ttu-id="a5beb-169">В результате выполнение продолжается до следующей точки останова, а при ее отсутствии — до конца сценария.</span><span class="sxs-lookup"><span data-stu-id="a5beb-169">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="a5beb-170">Просмотр стека вызовов</span><span class="sxs-lookup"><span data-stu-id="a5beb-170">To view the call stack</span></span>

<span data-ttu-id="a5beb-171">Стек вызовов отображает текущее расположение выполнения в сценарии.</span><span class="sxs-lookup"><span data-stu-id="a5beb-171">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="a5beb-172">Если сценарий выполняется в функции, вызванной другой функцией, это отражается путем добавления строк в выходные данные.</span><span class="sxs-lookup"><span data-stu-id="a5beb-172">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="a5beb-173">В самой нижней строке отображается исходный сценарий и его строка, в которой была вызвана функция.</span><span class="sxs-lookup"><span data-stu-id="a5beb-173">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="a5beb-174">Предыдущая строка показывает эту функцию и ее строку, в которой могла быть вызвана другая функция.</span><span class="sxs-lookup"><span data-stu-id="a5beb-174">The next line up shows that function and the line in it in which another function might have been called.</span></span> <span data-ttu-id="a5beb-175">В самой верхней строке отображается текущий контекст для текущей строки, в которой задана точка останова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-175">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="a5beb-176">Чтобы просмотреть текущий стек вызовов, пока выполнение приостановлено, нажмите клавиши <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>D</kbd>, выберите команду **Display Call Stack** (Отображение стека вызовов) в меню **Debug** (Отладка) или введите `K` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-176">While paused, to see the current call stack, press <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>D</kbd> or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type `K` and then press <kbd>ENTER</kbd>.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="a5beb-177">Остановка отладки</span><span class="sxs-lookup"><span data-stu-id="a5beb-177">To stop debugging</span></span>

<span data-ttu-id="a5beb-178">Нажмите клавиши <kbd>SHIFT</kbd>+<kbd>F5</kbd>, выберите команду **Stop Debugger** (Остановить отладчик) в меню **Debug** (Отладка) или введите `Q` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-178">Press <kbd>SHIFT</kbd>+<kbd>F5</kbd> or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type `Q` and then press <kbd>ENTER</kbd>.</span></span>

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a><span data-ttu-id="a5beb-179">Выполнение шагов с обходом, заходом и выходом во время отладки</span><span class="sxs-lookup"><span data-stu-id="a5beb-179">How to step over, step into, and step out while debugging</span></span>

<span data-ttu-id="a5beb-180">Пошаговое выполнение сценария — это поочередное выполнение его операторов.</span><span class="sxs-lookup"><span data-stu-id="a5beb-180">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="a5beb-181">Выполнение можно остановить на любой строке кода, чтобы проверить значения переменных и состояние системы.</span><span class="sxs-lookup"><span data-stu-id="a5beb-181">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="a5beb-182">В следующей таблице описаны задачи, часто выполняемые при отладке, такие как шаги с обходом, заходом и выходом:</span><span class="sxs-lookup"><span data-stu-id="a5beb-182">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="a5beb-183">Задача отладки</span><span class="sxs-lookup"><span data-stu-id="a5beb-183">Debugging Task</span></span> |                                                                                                                   <span data-ttu-id="a5beb-184">Description</span><span class="sxs-lookup"><span data-stu-id="a5beb-184">Description</span></span>                                                                                                                    |                                                      <span data-ttu-id="a5beb-185">Способ выполнения в интегрированной среде сценариев PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5beb-185">How to accomplish it in PowerShell ISE</span></span>                                                       |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="a5beb-186">**Шаг с заходом**</span><span class="sxs-lookup"><span data-stu-id="a5beb-186">**Step Into**</span></span>  | <span data-ttu-id="a5beb-187">Выполняет текущий оператор и останавливается на следующем операторе.</span><span class="sxs-lookup"><span data-stu-id="a5beb-187">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="a5beb-188">Если текущий оператор является вызовом функции или сценария, отладчик выполняет их по шагам. В противном случае он останавливается на следующем операторе.</span><span class="sxs-lookup"><span data-stu-id="a5beb-188">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span>                      | <span data-ttu-id="a5beb-189">Нажмите клавишу <kbd>F11</kbd>, выберите **Step Into** (Шаг с заходом) в меню **Debug** (Отладка) или введите `S` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-189">Press <kbd>F11</kbd> or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type `S` and press <kbd>ENTER</kbd>.</span></span>                 |
| <span data-ttu-id="a5beb-190">**Шаг с обходом**</span><span class="sxs-lookup"><span data-stu-id="a5beb-190">**Step Over**</span></span>  | <span data-ttu-id="a5beb-191">Выполняет текущий оператор и останавливается на следующем операторе.</span><span class="sxs-lookup"><span data-stu-id="a5beb-191">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="a5beb-192">Если текущий оператор является вызовом функции или сценария, отладчик выполняет их полностью и останавливается на операторе, следующем после этого вызова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-192">If the current statement is a function or script call, then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="a5beb-193">Нажмите клавишу <kbd>F10</kbd>, выберите **Step Over** (Шаг с обходом) в меню **Debug** (Отладка) или введите `V` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-193">Press <kbd>F10</kbd> or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type `V` and press <kbd>ENTER</kbd>.</span></span>                 |
| <span data-ttu-id="a5beb-194">**Шаг с выходом**</span><span class="sxs-lookup"><span data-stu-id="a5beb-194">**Step Out**</span></span>   | <span data-ttu-id="a5beb-195">Выходит из текущей функции и переходит на один уровень выше, если функция является вложенной.</span><span class="sxs-lookup"><span data-stu-id="a5beb-195">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="a5beb-196">Если выполняется тело главной функции, сценарий выполняется до конца или до следующей точки останова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-196">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="a5beb-197">Пропущенные операторы выполняются, но в них отладчик не останавливается.</span><span class="sxs-lookup"><span data-stu-id="a5beb-197">The skipped statements are executed, but not stepped through.</span></span>                   | <span data-ttu-id="a5beb-198">Нажмите клавиши <kbd>SHIFT</kbd>+<kbd>F11</kbd>, выберите команду **Step Out** (Шаг с выходом) в меню **Debug** (Отладка) или введите `O` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-198">Press <kbd>SHIFT</kbd>+<kbd>F11</kbd>, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type `O` and press <kbd>ENTER</kbd>.</span></span> |
| <span data-ttu-id="a5beb-199">**Продолжить**</span><span class="sxs-lookup"><span data-stu-id="a5beb-199">**Continue**</span></span>   | <span data-ttu-id="a5beb-200">Продолжает выполнение до конца или до следующей точки останова.</span><span class="sxs-lookup"><span data-stu-id="a5beb-200">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="a5beb-201">Пропущенные функции и вызовы выполняются, но в них отладчик не останавливается.</span><span class="sxs-lookup"><span data-stu-id="a5beb-201">The skipped functions and invocations are executed, but not stepped through.</span></span>                                                                                                          | <span data-ttu-id="a5beb-202">Нажмите клавишу <kbd>F5</kbd>, выберите **Run/Continue** (Выполнить/продолжить) в меню **Debug** (Отладка) или введите `C` в области консоли и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-202">Press <kbd>F5</kbd> or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type `C` and press <kbd>ENTER</kbd>.</span></span>               |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a><span data-ttu-id="a5beb-203">Отображение значений переменных при отладке</span><span class="sxs-lookup"><span data-stu-id="a5beb-203">How to display the values of variables while debugging</span></span>

<span data-ttu-id="a5beb-204">При пошаговом выполнении кода можно отобразить текущие значения переменных в сценарии.</span><span class="sxs-lookup"><span data-stu-id="a5beb-204">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="a5beb-205">Отображение значений стандартных переменных</span><span class="sxs-lookup"><span data-stu-id="a5beb-205">To display the values of standard variables</span></span>

<span data-ttu-id="a5beb-206">Используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="a5beb-206">Use one of the following methods:</span></span>

- <span data-ttu-id="a5beb-207">В области сценариев наведите указатель на переменную, чтобы отобразить ее значение в подсказке.</span><span class="sxs-lookup"><span data-stu-id="a5beb-207">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

- <span data-ttu-id="a5beb-208">В области консоли введите имя переменной и нажмите клавишу <kbd>ВВОД</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a5beb-208">In the Console Pane, type the variable name and press <kbd>ENTER</kbd>.</span></span>

<span data-ttu-id="a5beb-209">Все области в интегрированной среде сценариев всегда относятся к одной области действия.</span><span class="sxs-lookup"><span data-stu-id="a5beb-209">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="a5beb-210">Таким образом, при отладке сценария команды, вводимые в области консоли, выполняются в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="a5beb-210">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="a5beb-211">Это позволяет использовать область консоли для поиска значений переменных и вызова функций, которые определены только в сценарии.</span><span class="sxs-lookup"><span data-stu-id="a5beb-211">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="a5beb-212">Отображение значений автоматических переменных</span><span class="sxs-lookup"><span data-stu-id="a5beb-212">To display the values of automatic variables</span></span>

<span data-ttu-id="a5beb-213">Описанный выше метод позволяет отобразить значения почти всех переменных при отладке сценария.</span><span class="sxs-lookup"><span data-stu-id="a5beb-213">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="a5beb-214">Однако он не работает для следующих автоматических переменных:</span><span class="sxs-lookup"><span data-stu-id="a5beb-214">However, these methods do not work for the following automatic variables.</span></span>

- `$_`

- `$Input`

- `$MyInvocation`

- `$PSBoundParameters`

- `$Args`

<span data-ttu-id="a5beb-215">При попытке отобразить значение любой из этих переменных отображается значение переменной из внутреннего конвейера отладчика, а не переменной в сценарии.</span><span class="sxs-lookup"><span data-stu-id="a5beb-215">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="a5beb-216">Для некоторых переменных (`$_`, `$Input`, `$MyInvocation`, `$PSBoundParameters` и `$Args`) это можно обойти с помощью следующего метода.</span><span class="sxs-lookup"><span data-stu-id="a5beb-216">You can work around this for a few variables (`$_`, `$Input`, `$MyInvocation`, `$PSBoundParameters`, and `$Args`) by using the following method:</span></span>

1. <span data-ttu-id="a5beb-217">Присвойте значение автоматической переменной в сценарии новой переменной.</span><span class="sxs-lookup"><span data-stu-id="a5beb-217">In the script, assign the value of the automatic variable to a new variable.</span></span>

1. <span data-ttu-id="a5beb-218">Отобразите значение новой переменной, наведя на нее указатель мыши в области сценариев или введя ее имя в области консоли.</span><span class="sxs-lookup"><span data-stu-id="a5beb-218">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="a5beb-219">Например, чтобы отобразить значение переменной `$MyInvocation` в сценарии, присвойте ее значение новой переменной, например `$scriptName`, а затем наведите указатель мыши на переменную `$scriptName` или введите ее для отображения значения.</span><span class="sxs-lookup"><span data-stu-id="a5beb-219">For example, to display the value of the `$MyInvocation` variable, in the script, assign the value to a new variable, such as `$scriptName`, and then hover over or type the `$scriptName` variable to display its value.</span></span>

```powershell
# In C:\ps-test\MyScript.ps1
$scriptName = $MyInvocation.MyCommand.Path
```

```PowerShell
# In the Console Pane:
.\MyScript.ps1
$scriptName
```

```Output
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a><span data-ttu-id="a5beb-220">См. также:</span><span class="sxs-lookup"><span data-stu-id="a5beb-220">See Also</span></span>

[<span data-ttu-id="a5beb-221">Обзор интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5beb-221">Exploring the Windows PowerShell ISE</span></span>](exploring-the-windows-powershell-ise.md)
