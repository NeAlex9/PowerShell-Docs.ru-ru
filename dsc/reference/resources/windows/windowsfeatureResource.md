---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс WindowsFeature в DSC
ms.openlocfilehash: 7a57f4b2797ab3bb202aea8b2543d1e3f14074e9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076707"
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="ca330-103">Ресурс WindowsFeature в DSC</span><span class="sxs-lookup"><span data-stu-id="ca330-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="ca330-104">Область применения. Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ca330-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="ca330-105">Ресурс **WindowsFeature** в DSC Windows PowerShell предоставляет механизм добавления и удаления ролей и компонентов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="ca330-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="ca330-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ca330-106">Syntax</span></span>

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="ca330-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="ca330-107">Properties</span></span>

|  <span data-ttu-id="ca330-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="ca330-108">Property</span></span>  |  <span data-ttu-id="ca330-109">Описание</span><span class="sxs-lookup"><span data-stu-id="ca330-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="ca330-110">Name</span><span class="sxs-lookup"><span data-stu-id="ca330-110">Name</span></span>| <span data-ttu-id="ca330-111">Указывает имя роли или компонента, которые необходимо добавить или удалить.</span><span class="sxs-lookup"><span data-stu-id="ca330-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="ca330-112">Это свойство аналогично свойству __Name__ командлета [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) и не является отображаемым именем роли или компонента.</span><span class="sxs-lookup"><span data-stu-id="ca330-112">This is the same as the __Name__ property from the [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) cmdlet, and not the display name of the role or feature.</span></span>|
| <span data-ttu-id="ca330-113">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="ca330-113">Credential</span></span>| <span data-ttu-id="ca330-114">Указывает учетные данные для добавления или удаления роли или компонента.</span><span class="sxs-lookup"><span data-stu-id="ca330-114">Indicates the credentials to use to add or remove the role or feature.</span></span>|
| <span data-ttu-id="ca330-115">Ensure</span><span class="sxs-lookup"><span data-stu-id="ca330-115">Ensure</span></span>| <span data-ttu-id="ca330-116">Указывает, добавляется или удаляется роль или компонент.</span><span class="sxs-lookup"><span data-stu-id="ca330-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="ca330-117">Чтобы добавить роль или компонент, установите это свойство равным Present, чтобы удалить — равным Absent.</span><span class="sxs-lookup"><span data-stu-id="ca330-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="ca330-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="ca330-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="ca330-119">Присвойте этому свойству значение __$true__ для синхронизации состояния всех необходимых дополнительных компонентов с состоянием компонента, указанного в свойстве __Name__.</span><span class="sxs-lookup"><span data-stu-id="ca330-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>|
| <span data-ttu-id="ca330-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="ca330-120">LogPath</span></span>| <span data-ttu-id="ca330-121">Указывает путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.</span><span class="sxs-lookup"><span data-stu-id="ca330-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="ca330-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="ca330-122">DependsOn</span></span>| <span data-ttu-id="ca330-123">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="ca330-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ca330-124">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ca330-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="ca330-125">Источник</span><span class="sxs-lookup"><span data-stu-id="ca330-125">Source</span></span>| <span data-ttu-id="ca330-126">Указывает расположение исходного файла для установки, если он необходим.</span><span class="sxs-lookup"><span data-stu-id="ca330-126">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="ca330-127">Пример</span><span class="sxs-lookup"><span data-stu-id="ca330-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present"
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature
}
```