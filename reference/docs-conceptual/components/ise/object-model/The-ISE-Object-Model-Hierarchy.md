---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Иерархия объектной модели интегрированной среды сценариев
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057729"
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="1c2ca-103">Иерархия объектной модели интегрированной среды сценариев</span><span class="sxs-lookup"><span data-stu-id="1c2ca-103">The ISE Object Model Hierarchy</span></span>

<span data-ttu-id="1c2ca-104">В этом разделе демонстрируется иерархия объектов, которые входят в состав интегрированной среды сценариев Windows PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span>
<span data-ttu-id="1c2ca-105">Интегрированная среда сценариев Windows PowerShell входит в состав Windows PowerShell 3.0 и Windows PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span>
<span data-ttu-id="1c2ca-106">Щелкните объект, чтобы перейти к справочной документации для класса, определяющего объект.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

## <a name="psise-object"></a><span data-ttu-id="1c2ca-107">Объект $psISE</span><span class="sxs-lookup"><span data-stu-id="1c2ca-107">$psISE Object</span></span>

<span data-ttu-id="1c2ca-108">Объект **$psISE** — это [корневой объект](The-ObjectModelRoot-Object.md) иерархии объектов интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span>
<span data-ttu-id="1c2ca-109">Располагаясь на верхнем уровне, он предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="1c2ca-109">Located at the top level, it makes the following objects available for scripting:</span></span>

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[<span data-ttu-id="1c2ca-110">$psISE.CurrentFile</span><span class="sxs-lookup"><span data-stu-id="1c2ca-110">$psISE.CurrentFile</span></span>](The-ISEFile-Object.md)

<span data-ttu-id="1c2ca-111">Объект **$PsISE.CurrentFile** является экземпляром класса [ISEFile](The-ISEFile-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-111">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class.</span></span>

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[<span data-ttu-id="1c2ca-112">$psISE.CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="1c2ca-112">$psISE.CurrentPowerShellTab</span></span>](The-PowerShellTab-Object.md)

<span data-ttu-id="1c2ca-113">Объект **$psISE.CurrentPowerShellTab** является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-113">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="1c2ca-114">$psISE.CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="1c2ca-114">$psISE.CurrentVisibleHorizontalTool</span></span>

<span data-ttu-id="1c2ca-115">Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-115">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="1c2ca-116">Он представляет установленную надстройку, закрепленную в верхней части окна интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-116">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span>

## <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="1c2ca-117">$psISE.CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="1c2ca-117">$psISE.CurrentVisibleVerticalTool</span></span>

<span data-ttu-id="1c2ca-118">Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-118">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="1c2ca-119">Он представляет установленную надстройку, закрепленную в правой части окна интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-119">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span>

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[<span data-ttu-id="1c2ca-120">$psISE.Options</span><span class="sxs-lookup"><span data-stu-id="1c2ca-120">$psISE.Options</span></span>](The-ISEOptions-Object.md)

<span data-ttu-id="1c2ca-121">Объект **$PsISE.Options** является экземпляром класса [ISEOptions](The-ISEOptions-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-121">The **$psISE.Options** object is an instance of the [ISEOptions](The-ISEOptions-Object.md) class.</span></span>
<span data-ttu-id="1c2ca-122">Объект ISEOptions представляет различные параметры для интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-122">The ISEOptions object represents various settings for Windows PowerShell ISE.</span></span>
<span data-ttu-id="1c2ca-123">Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEOptions.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-123">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEOptions class.</span></span>

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[<span data-ttu-id="1c2ca-124">$psISE.PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="1c2ca-124">$psISE.PowerShellTabs</span></span>](The-PowerShellTabCollection-Object.md)

<span data-ttu-id="1c2ca-125">Объект **$PsISE.PowerShellTabs** является экземпляром класса [PowerShellTabCollection](The-PowerShellTabCollection-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-125">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span>
<span data-ttu-id="1c2ca-126">Это коллекция всех открытых вкладок PowerShell, представляющих доступные среды выполнения Windows PowerShell на локальном компьютере или на подключенных удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="1c2ca-126">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span>
<span data-ttu-id="1c2ca-127">Каждый элемент в коллекции является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1c2ca-127">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c2ca-128">См. также</span><span class="sxs-lookup"><span data-stu-id="1c2ca-128">See Also</span></span>

- [<span data-ttu-id="1c2ca-129">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c2ca-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="1c2ca-130">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="1c2ca-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)