---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс DSC WindowsOptionalFeature
ms.openlocfilehash: 1866bc9cd2194a62de23eaabee8a9c5049a84946
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219408"
---
# <a name="dsc-windowsoptionalfeature-resource"></a><span data-ttu-id="88052-103">Ресурс DSC WindowsOptionalFeature</span><span class="sxs-lookup"><span data-stu-id="88052-103">DSC WindowsOptionalFeature Resource</span></span>

> <span data-ttu-id="88052-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="88052-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="88052-105">Ресурс **WindowsOptionalFeature** в DSC Windows PowerShell предоставляет механизм включения дополнительных компонентов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="88052-105">The **WindowsOptionalFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="88052-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="88052-106">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="88052-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="88052-107">Properties</span></span>

|  <span data-ttu-id="88052-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="88052-108">Property</span></span>  |  <span data-ttu-id="88052-109">Описание</span><span class="sxs-lookup"><span data-stu-id="88052-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="88052-110">Name</span><span class="sxs-lookup"><span data-stu-id="88052-110">Name</span></span>| <span data-ttu-id="88052-111">Указывает имя компонента, который необходимо включить или отключить.</span><span class="sxs-lookup"><span data-stu-id="88052-111">Indicates the name of the feature that you want to ensure is enabled or disabled.</span></span>|
| <span data-ttu-id="88052-112">Ensure</span><span class="sxs-lookup"><span data-stu-id="88052-112">Ensure</span></span>| <span data-ttu-id="88052-113">Указывает, включен ли компонент.</span><span class="sxs-lookup"><span data-stu-id="88052-113">Specifies whether the feature is enabled.</span></span> <span data-ttu-id="88052-114">Чтобы включить компонент, установите для этого свойства значение "Включить", чтобы отключить — значение "Отключить".</span><span class="sxs-lookup"><span data-stu-id="88052-114">To ensure that the feature is enabled, set this property to "Enable" To ensure that the feature is disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="88052-115">Источник</span><span class="sxs-lookup"><span data-stu-id="88052-115">Source</span></span>| <span data-ttu-id="88052-116">Не реализовано.</span><span class="sxs-lookup"><span data-stu-id="88052-116">Not implemented.</span></span>|
| <span data-ttu-id="88052-117">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="88052-117">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="88052-118">Указывает, обращается ли система DISM к Центру обновления Windows при поиске исходных файлов для включения компонента.</span><span class="sxs-lookup"><span data-stu-id="88052-118">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable a feature.</span></span> <span data-ttu-id="88052-119">Если задано значение $true, система DISM не обращается к Центру обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="88052-119">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="88052-120">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="88052-120">RemoveFilesOnDisable</span></span>| <span data-ttu-id="88052-121">Задайте значение **$true**, чтобы удалить все файлы, связанные с компонентом, при его отключении (то есть когда свойству **Ensure** присваивается значение Absent).</span><span class="sxs-lookup"><span data-stu-id="88052-121">Set to **$true** to remove all files associated with the feature when it is disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="88052-122">Уровень журнала</span><span class="sxs-lookup"><span data-stu-id="88052-122">LogLevel</span></span>| <span data-ttu-id="88052-123">Максимальный уровень результатов, показываемый в журналах.</span><span class="sxs-lookup"><span data-stu-id="88052-123">The maximum output level shown in the logs.</span></span> <span data-ttu-id="88052-124">Допустимые значения: ErrorsOnly (в журналы записываются только ошибки), ErrorsAndWarning (в журналы записываются ошибки и предупреждения) и ErrorsAndWarningAndInformation (в журналы записываются ошибки, предупреждения и отладочные сведения).</span><span class="sxs-lookup"><span data-stu-id="88052-124">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="88052-125">LogPath</span><span class="sxs-lookup"><span data-stu-id="88052-125">LogPath</span></span>| <span data-ttu-id="88052-126">Путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.</span><span class="sxs-lookup"><span data-stu-id="88052-126">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="88052-127">DependsOn</span><span class="sxs-lookup"><span data-stu-id="88052-127">DependsOn</span></span>| <span data-ttu-id="88052-128">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="88052-128">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="88052-129">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="88052-129">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|