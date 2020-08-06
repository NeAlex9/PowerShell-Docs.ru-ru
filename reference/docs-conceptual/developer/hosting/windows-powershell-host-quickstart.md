---
title: Краткое руководство по узлу Windows PowerShell | Документация Майкрософт
ms.date: 09/12/2016
ms.openlocfilehash: fea6bd5ae49ecf552c583271ee9d869b1ccebae8
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/05/2020
ms.locfileid: "87779409"
---
# <a name="windows-powershell-host-quickstart"></a><span data-ttu-id="d42a7-102">Краткое руководство по узлам Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d42a7-102">Windows PowerShell Host Quickstart</span></span>

<span data-ttu-id="d42a7-103">Для размещения Windows PowerShell в приложении используется класс [System. Management. Automation. PowerShell](/dotnet/api/System.Management.Automation.PowerShell) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-103">To host Windows PowerShell in your application, you use the [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) class.</span></span>
<span data-ttu-id="d42a7-104">Этот класс предоставляет методы, которые создают конвейер команд, а затем выполняют эти команды в пространстве выполнения.</span><span class="sxs-lookup"><span data-stu-id="d42a7-104">This class provides methods that create a pipeline of commands and then execute those commands in a runspace.</span></span>
<span data-ttu-id="d42a7-105">Самый простой способ создать ведущее приложение — использовать пространство выполнения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d42a7-105">The simplest way to create a host application is to use the default runspace.</span></span>
<span data-ttu-id="d42a7-106">Пространство выполнения по умолчанию содержит все основные команды Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d42a7-106">The default runspace contains all of the core Windows PowerShell commands.</span></span>
<span data-ttu-id="d42a7-107">Если требуется, чтобы приложение предоставляло только подмножество команд Windows PowerShell, необходимо создать пользовательское пространство выполнения.</span><span class="sxs-lookup"><span data-stu-id="d42a7-107">If you want your application to expose only a subset of the Windows PowerShell commands, you must create a custom runspace.</span></span>

## <a name="using-the-default-runspace"></a><span data-ttu-id="d42a7-108">Использование пространства выполнения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d42a7-108">Using the default runspace</span></span>

<span data-ttu-id="d42a7-109">Для начала мы используем пространство выполнения по умолчанию и с помощью методов класса [System. Management. Automation. PowerShell](/dotnet/api/System.Management.Automation.PowerShell) добавим команды, параметры, инструкции и скрипты в конвейер.</span><span class="sxs-lookup"><span data-stu-id="d42a7-109">To start, we'll use the default runspace, and use the methods of the [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) class to add commands, parameters, statements, and scripts to a pipeline.</span></span>

### <a name="addcommand"></a><span data-ttu-id="d42a7-110">AddCommand</span><span class="sxs-lookup"><span data-stu-id="d42a7-110">AddCommand</span></span>

<span data-ttu-id="d42a7-111">Для добавления команд в конвейер используется метод [System. Management. Automation. PowerShell. AddCommand](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-111">You use the [System.Management.Automation.Powershell.AddCommand](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) method to add commands to the pipeline.</span></span>
<span data-ttu-id="d42a7-112">Например, предположим, что требуется получить список запущенных процессов на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d42a7-112">For example, suppose you want to get the list of running processes on the machine.</span></span>
<span data-ttu-id="d42a7-113">Ниже приведен способ выполнения этой команды.</span><span class="sxs-lookup"><span data-stu-id="d42a7-113">The way to run this command is as follows.</span></span>

1. <span data-ttu-id="d42a7-114">Создайте объект [System. Management. Automation. PowerShell](/dotnet/api/System.Management.Automation.PowerShell) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-114">Create a [System.Management.Automation.PowerShell](/dotnet/api/System.Management.Automation.PowerShell) object.</span></span>

   ```csharp
   PowerShell ps = PowerShell.Create();
   ```

2. <span data-ttu-id="d42a7-115">Добавьте команду, которую требуется выполнить.</span><span class="sxs-lookup"><span data-stu-id="d42a7-115">Add the command that you want to execute.</span></span>

   ```csharp
   ps.AddCommand("Get-Process");
   ```

3. <span data-ttu-id="d42a7-116">Вызовите команду.</span><span class="sxs-lookup"><span data-stu-id="d42a7-116">Invoke the command.</span></span>

   ```csharp
   ps.Invoke();
   ```

<span data-ttu-id="d42a7-117">Если метод AddCommand вызывается несколько раз перед вызовом метода [System. Management. Automation. PowerShell. Invoke](/dotnet/api/System.Management.Automation.PowerShell.Invoke) , результат первой команды передается второму и т. д.</span><span class="sxs-lookup"><span data-stu-id="d42a7-117">If you call the AddCommand method more than once before you call the [System.Management.Automation.Powershell.Invoke](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method, the result of the first command is piped to the second, and so on.</span></span>
<span data-ttu-id="d42a7-118">Если вы не хотите передавать результат предыдущей команды команде, добавьте ее, вызвав метод [System. Management. Automation. PowerShell. аддстатемент](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-118">If you do not want to pipe the result of a previous command to a command, add it by calling the [System.Management.Automation.Powershell.AddStatement](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) instead.</span></span>

### <a name="addparameter"></a><span data-ttu-id="d42a7-119">аддпараметер</span><span class="sxs-lookup"><span data-stu-id="d42a7-119">AddParameter</span></span>

<span data-ttu-id="d42a7-120">В предыдущем примере выполняется одна команда без параметров.</span><span class="sxs-lookup"><span data-stu-id="d42a7-120">The previous example executes a single command without any parameters.</span></span>
<span data-ttu-id="d42a7-121">В команду можно добавить параметры с помощью метода [System. Management. Automation. пскомманд. аддпараметер](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-121">You can add parameters to the command by using the [System.Management.Automation.PSCommand.AddParameter](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) method.</span></span>
<span data-ttu-id="d42a7-122">Например, следующий код возвращает список всех процессов, имена которых `PowerShell` выполняются на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d42a7-122">For example, the following code gets a list of all of the processes that are named `PowerShell` running on the machine.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .Invoke();
```

<span data-ttu-id="d42a7-123">Можно добавить дополнительные параметры путем многократного вызова метода Аддпараметер.</span><span class="sxs-lookup"><span data-stu-id="d42a7-123">You can add additional parameters by calling the AddParameter method repeatedly.</span></span>

```csharp                   
PowerShell.Create().AddCommand("Get-ChildItem")
                   .AddParameter("Path", @"c:\Windows")
                   .AddParameter("Filter", "*.exe")
                   .Invoke();
```

<span data-ttu-id="d42a7-124">Также можно добавить словарь имен и значений параметров, вызвав метод [System. Management. Automation. PowerShell. аддпараметерс](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-124">You can also add a dictionary of parameter names and values by calling the [System.Management.Automation.PowerShell.AddParameters](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) method.</span></span>

```csharp
IDictionary parameters = new Dictionary<String, String>();
parameters.Add("Path", @"c:\Windows");
parameters.Add("Filter", "*.exe");

PowerShell.Create().AddCommand("Get-Process")
   .AddParameters(parameters)
      .Invoke()

```

### <a name="addstatement"></a><span data-ttu-id="d42a7-125">аддстатемент</span><span class="sxs-lookup"><span data-stu-id="d42a7-125">AddStatement</span></span>

<span data-ttu-id="d42a7-126">Пакетную обработку можно имитировать с помощью метода [System. Management. Automation. PowerShell. аддстатемент](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) , который добавляет дополнительный оператор в конец конвейера.</span><span class="sxs-lookup"><span data-stu-id="d42a7-126">You can simulate batching by using the [System.Management.Automation.PowerShell.AddStatement](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) method, which adds an additional statement to the end of the pipeline.</span></span>
<span data-ttu-id="d42a7-127">Следующий код возвращает список запущенных процессов с именем `PowerShell` , а затем получает список запущенных служб.</span><span class="sxs-lookup"><span data-stu-id="d42a7-127">The following code gets a list of running processes with the name `PowerShell`, and then gets the list of running services.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddCommand("Get-Process").AddParameter("Name", "PowerShell");
ps.AddStatement().AddCommand("Get-Service");
ps.Invoke();
```

### <a name="addscript"></a><span data-ttu-id="d42a7-128">аддскрипт</span><span class="sxs-lookup"><span data-stu-id="d42a7-128">AddScript</span></span>

<span data-ttu-id="d42a7-129">Можно запустить существующий скрипт, вызвав метод [System. Management. Automation. PowerShell. аддскрипт](/dotnet/api/System.Management.Automation.PowerShell.AddScript) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-129">You can run an existing script by calling the [System.Management.Automation.PowerShell.AddScript](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method.</span></span>
<span data-ttu-id="d42a7-130">В следующем примере в конвейер добавляется скрипт и выполняется его выполнение.</span><span class="sxs-lookup"><span data-stu-id="d42a7-130">The following example adds a script to the pipeline and runs it.</span></span>
<span data-ttu-id="d42a7-131">В этом примере предполагается, что в папке уже есть скрипт с именем `MyScript.ps1` `D:\PSScripts` .</span><span class="sxs-lookup"><span data-stu-id="d42a7-131">This example assumes there is already a script named `MyScript.ps1` in a folder named `D:\PSScripts`.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript("D:\PSScripts\MyScript.ps1").Invoke();
```

<span data-ttu-id="d42a7-132">Существует также версия метода Аддскрипт, принимающая логический параметр с именем `useLocalScope` .</span><span class="sxs-lookup"><span data-stu-id="d42a7-132">There is also a version of the AddScript method that takes a boolean parameter named `useLocalScope`.</span></span>
<span data-ttu-id="d42a7-133">Если этот параметр имеет значение `true` , скрипт выполняется в локальной области.</span><span class="sxs-lookup"><span data-stu-id="d42a7-133">If this parameter is set to `true`, then the script is run in the local scope.</span></span>
<span data-ttu-id="d42a7-134">Следующий код запустит скрипт в локальной области.</span><span class="sxs-lookup"><span data-stu-id="d42a7-134">The following code will run the script in the local scope.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript(@"D:\PSScripts\MyScript.ps1", true).Invoke();
```

## <a name="creating-a-custom-runspace"></a><span data-ttu-id="d42a7-135">Создание пользовательского пространства выполнения</span><span class="sxs-lookup"><span data-stu-id="d42a7-135">Creating a custom runspace</span></span>

<span data-ttu-id="d42a7-136">Хотя пространство выполнения по умолчанию, используемое в предыдущих примерах, загружает все основные команды Windows PowerShell, можно создать пользовательское пространство выполнения, которое загружает только указанное подмножество команд.</span><span class="sxs-lookup"><span data-stu-id="d42a7-136">While the default runspace used in the previous examples loads all of the core Windows PowerShell commands, you can create a custom runspace that loads only a specified subset of all commands.</span></span>
<span data-ttu-id="d42a7-137">Это может потребоваться для повышения производительности (загрузка большего количества команд — снижение производительности) или ограничение возможности пользователя выполнять операции.</span><span class="sxs-lookup"><span data-stu-id="d42a7-137">You might want to do this to improve performance (loading a larger number of commands is a performance hit), or to restrict the capability of the user to perform operations.</span></span>
<span data-ttu-id="d42a7-138">Пространство выполнения, предоставляющее только ограниченное количество команд, называется ограниченным пространством выполнения.</span><span class="sxs-lookup"><span data-stu-id="d42a7-138">A runspace that exposes only a limited number of commands is called a constrained runspace.</span></span>
<span data-ttu-id="d42a7-139">Для создания ограниченного пространства выполнения используйте классы [System. Management. Automation. пространства выполнения](/dotnet/api/System.Management.Automation.Runspaces.Runspace) и [System.Management.Automation.Runspaces.Iniтиалсессионстате](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-139">To create a constrained runspace, you use the [System.Management.Automation.Runspaces.Runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) and [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) classes.</span></span>

### <a name="creating-an-initialsessionstate-object"></a><span data-ttu-id="d42a7-140">Создание объекта InitialSessionState</span><span class="sxs-lookup"><span data-stu-id="d42a7-140">Creating an InitialSessionState object</span></span>

<span data-ttu-id="d42a7-141">Чтобы создать пользовательское пространство выполнения, необходимо сначала создать объект [System.Management.Automation.Runspaces.Iniтиалсессионстате](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-141">To create a custom runspace, you must first create an [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object.</span></span>
<span data-ttu-id="d42a7-142">В следующем примере для создания пространства выполнения после создания объекта InitialSessionState по умолчанию мы используем [System. Management. Automation. пространства. рунспацефактори](/dotnet/api/System.Management.Automation.Runspaces.RunspaceFactory) .</span><span class="sxs-lookup"><span data-stu-id="d42a7-142">In the following example, we use the [System.Management.Automation.Runspaces.RunspaceFactory](/dotnet/api/System.Management.Automation.Runspaces.RunspaceFactory) to create a runspace after creating a default InitialSessionState object.</span></span>

```csharp
InitialSessionState iss = InitialSessionState.CreateDefault();
Runspace rs = RunspaceFactory.CreateRunspace(iss);
rs.Open();
PowerShell ps = PowerShell.Create();
ps.Runspace = rs;
ps.AddCommand("Get-Command");
ps.Invoke();
```

### <a name="constraining-the-runspace"></a><span data-ttu-id="d42a7-143">Ограничение пространства выполнения</span><span class="sxs-lookup"><span data-stu-id="d42a7-143">Constraining the runspace</span></span>

<span data-ttu-id="d42a7-144">В предыдущем примере мы создали объект [System.Management.Automation.Runspaces.Iniтиалсессионстате](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) по умолчанию, который загружает все встроенные основные ядра Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d42a7-144">In the previous example, we created a default [System.Management.Automation.Runspaces.InitialSessionState](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object that loads all of the built-in core Windows PowerShell.</span></span>
<span data-ttu-id="d42a7-145">Мы также могли вызвать метод [System.Management.Automation.Runspaces.Iniтиалсессионстате. CreateDefault2](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) , чтобы создать объект InitialSessionState, который будет загружать только команды в оснастке Microsoft. PowerShell. Core.</span><span class="sxs-lookup"><span data-stu-id="d42a7-145">We could also have called the [System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.CreateDefault2) method to create an InitialSessionState object that would load only the commands in the Microsoft.PowerShell.Core snapin.</span></span>
<span data-ttu-id="d42a7-146">Чтобы создать более ограниченное пространство выполнения, необходимо создать пустой объект InitialSessionState, вызвав метод [System.Management.Automation.Runspaces.Iniтиалсессионстате. Create](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.Create) , а затем добавить команды в InitialSessionState.</span><span class="sxs-lookup"><span data-stu-id="d42a7-146">To create a more constrained runspace, you must create an empty InitialSessionState object by calling the [System.Management.Automation.Runspaces.InitialSessionState.Create](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState.Create) method, and then add commands to the InitialSessionState.</span></span>

<span data-ttu-id="d42a7-147">Использование пространства выполнения, которое загружает только указанные команды, обеспечивает значительно повышенную производительность.</span><span class="sxs-lookup"><span data-stu-id="d42a7-147">Using a runspace that loads only the commands that you specify provides significantly improved performance.</span></span>

<span data-ttu-id="d42a7-148">Методы класса [System. Management. Automation. пространства выполнения. сессионстатекмдлетентри](/dotnet/api/System.Management.Automation.Runspaces.SessionStateCmdletEntry) используются для определения командлетов для начального состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="d42a7-148">You use the methods of the [System.Management.Automation.Runspaces.SessionStateCmdletEntry](/dotnet/api/System.Management.Automation.Runspaces.SessionStateCmdletEntry) class to define cmdlets for the initial session state.</span></span>
<span data-ttu-id="d42a7-149">В следующем примере создается пустое начальное состояние сеанса, затем определяется и добавляются `Get-Command` `Import-Module` команды и в исходное состояние сеанса.</span><span class="sxs-lookup"><span data-stu-id="d42a7-149">The following example creates an empty initial session state, then defines and adds the `Get-Command` and `Import-Module` commands to the initial session state.</span></span>
<span data-ttu-id="d42a7-150">Затем создается пространство выполнения, ограниченное этим начальным состоянием сеанса, и выполняются команды в этом пространстве выполнения.</span><span class="sxs-lookup"><span data-stu-id="d42a7-150">We then create a runspace constrained by that initial session state, and execute the commands in that runspace.</span></span>

<span data-ttu-id="d42a7-151">Создайте начальное состояние сеанса.</span><span class="sxs-lookup"><span data-stu-id="d42a7-151">Create the initial session state.</span></span>

```csharp
InitialSessionState iss = InitialSessionState.Create();
```

<span data-ttu-id="d42a7-152">Определение и Добавление команд в исходное состояние сеанса.</span><span class="sxs-lookup"><span data-stu-id="d42a7-152">Define and add commands to the initial session state.</span></span>

```csharp
SessionStateCmdletEntry getCommand = new SessionStateCmdletEntry(
        "Get-Command", typeof(Microsoft.PowerShell.Commands.GetCommandCommand), "");
SessionStateCmdletEntry importModule = new SessionStateCmdletEntry(
        "Import-Module", typeof(Microsoft.PowerShell.Commands.ImportModuleCommand), "");
iss.Commands.Add(getCommand);
iss.Commands.Add(importModule);
```

<span data-ttu-id="d42a7-153">Создайте и откройте пространство выполнения.</span><span class="sxs-lookup"><span data-stu-id="d42a7-153">Create and open the runspace.</span></span>

```csharp
Runspace rs = RunspaceFactory.CreateRunspace(iss);
rs.Open();
```

<span data-ttu-id="d42a7-154">Выполните команду и отобразите результат.</span><span class="sxs-lookup"><span data-stu-id="d42a7-154">Execute a command and show the result.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.Runspace = rs;
ps.AddCommand("Get-Command");
Collection<CommandInfo> result = ps.Invoke<CommandInfo>();
foreach (var entry in result)
{
       Console.WriteLine(entry.Name);
}
```

<span data-ttu-id="d42a7-155">При запуске результат этого кода будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d42a7-155">When run, the output of this code will look as follows.</span></span>

```powershell
Get-Command
Import-Module
```
