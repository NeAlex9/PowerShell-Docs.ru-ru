---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEAddOnToolCollection"
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: 09088c9e7307a26b86e82f2dc10d2648213c6bd2
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="ef3b3-103">Объект ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="ef3b3-103">The ISEAddOnToolCollection Object</span></span>
  <span data-ttu-id="ef3b3-104">Объект **ISEAddOnToolCollection** — это коллекция объектов **ISEAddOnTool**.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="ef3b3-105">Примером является объект **$psISE.CurrentPowerShellTab.VerticalAddOnTools**.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="ef3b3-106">Методы</span><span class="sxs-lookup"><span data-stu-id="ef3b3-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="ef3b3-107">Add\( Name, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="ef3b3-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>
  <span data-ttu-id="ef3b3-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="ef3b3-109">Добавляет новую надстройку в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="ef3b3-110">Метод возвращает добавленную надстройку.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="ef3b3-111">Перед выполнением этой команды необходимо установить надстройку на локальном компьютере и загрузить сборку.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

 <span data-ttu-id="ef3b3-112">**Name** — строка. Задает отображаемое имя надстройки, добавляемой в интегрированную среду скриптов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

 <span data-ttu-id="ef3b3-113">**ControlType** — тип. Определяет добавляемый элемент управления.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-113">**ControlType** -Type Specifies the control that is added.</span></span>

 <span data-ttu-id="ef3b3-114">**\[IsVisible\]** — необязательный логический параметр. Если задано значение **$true**, надстройка сразу же отображается в связанной области инструментов.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```PowerShell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="ef3b3-115">Remove\( Item \)</span><span class="sxs-lookup"><span data-stu-id="ef3b3-115">Remove\( Item \)</span></span>
  <span data-ttu-id="ef3b3-116">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="ef3b3-117">Удаляет указанную надстройку из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-117">Removes the specified add-on tool from the collection.</span></span>

 <span data-ttu-id="ef3b3-118">**Item** — Microsoft.PowerShell.Host.ISE.ISEAddOnTool. Указывает объект, удаляемый из интегрированной среды скриптов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```PowerShell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="ef3b3-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="ef3b3-119">SetSelectedPowerShellTab\( psTab \)</span></span>
  <span data-ttu-id="ef3b3-120">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="ef3b3-121">Выбирает вкладку PowerShell, указанную параметром **psTab**.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

 <span data-ttu-id="ef3b3-122">**psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab. Выбираемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```PowerShell
      $newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

### <a name="remove-pstab-"></a><span data-ttu-id="ef3b3-123">Remove\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="ef3b3-123">Remove\( psTab \)</span></span>
  <span data-ttu-id="ef3b3-124">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="ef3b3-125">Удаляет вкладку PowerShell, указанную параметром **psTab**.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

 <span data-ttu-id="ef3b3-126">**psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab. Удаляемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef3b3-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```PowerShell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="ef3b3-127">См. также</span><span class="sxs-lookup"><span data-stu-id="ef3b3-127">See Also</span></span>
- [<span data-ttu-id="ef3b3-128">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="ef3b3-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="ef3b3-129">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef3b3-129">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="ef3b3-130">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef3b3-130">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="ef3b3-131">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="ef3b3-131">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  