---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс DSC ProcessSet
ms.openlocfilehash: 91a2d5b562864addcb8e11062916d291448bbf57
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047531"
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="8aa63-103">Ресурс WindowsProcess в DSC</span><span class="sxs-lookup"><span data-stu-id="8aa63-103">DSC WindowsProcess Resource</span></span>

<span data-ttu-id="8aa63-104">_Применяется к: Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="8aa63-104">_Applies To: Windows PowerShell 5.0_</span></span>

<span data-ttu-id="8aa63-105">Ресурс **ProcessSet** в DSC Windows PowerShell предоставляет механизм настройки процессов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="8aa63-105">The **ProcessSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span> <span data-ttu-id="8aa63-106">Он является [составным ресурсом](../../../resources/authoringResourceComposite.md), который вызывает [ресурс WindowsProcess](windowsProcessResource.md) для каждой группы, указанной в параметре `GroupName`.</span><span class="sxs-lookup"><span data-stu-id="8aa63-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsProcess resource](windowsProcessResource.md) for each group specified in the `GroupName` parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="8aa63-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="8aa63-107">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="8aa63-108">Свойства</span><span class="sxs-lookup"><span data-stu-id="8aa63-108">Properties</span></span>

| <span data-ttu-id="8aa63-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="8aa63-109">Property</span></span> | <span data-ttu-id="8aa63-110">Описание</span><span class="sxs-lookup"><span data-stu-id="8aa63-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa63-111">Аргументы</span><span class="sxs-lookup"><span data-stu-id="8aa63-111">Arguments</span></span>| <span data-ttu-id="8aa63-112">Строка, содержащая аргументы, которые будут переданы процессу "как есть".</span><span class="sxs-lookup"><span data-stu-id="8aa63-112">A string that contains arguments to pass to the process as-is.</span></span> <span data-ttu-id="8aa63-113">Если необходимо передать несколько аргументов, поместите их все в эту строку.</span><span class="sxs-lookup"><span data-stu-id="8aa63-113">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="8aa63-114">путь</span><span class="sxs-lookup"><span data-stu-id="8aa63-114">Path</span></span>| <span data-ttu-id="8aa63-115">Пути к исполняемым файлам процессов.</span><span class="sxs-lookup"><span data-stu-id="8aa63-115">The paths to the process executables.</span></span> <span data-ttu-id="8aa63-116">Если это имена исполняемых файлов (а не полные пути к ним), ресурс DSC будет искать переменную среды **Path** (`$env:Path`), чтобы найти файлы.</span><span class="sxs-lookup"><span data-stu-id="8aa63-116">If these are the names of the executable files (not fully qualified paths), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the files.</span></span> <span data-ttu-id="8aa63-117">Если значения этого свойства — полные пути, ресурс DSC не будет использовать переменную среды **Path** для поиска файлов и вызовет ошибку в случае отсутствия путей.</span><span class="sxs-lookup"><span data-stu-id="8aa63-117">If the values of this property are fully qualified paths, DSC will not use the **Path** environment variable to find the files, and will throw an error if any of the paths do not exist.</span></span> <span data-ttu-id="8aa63-118">Относительные пути не допускаются.</span><span class="sxs-lookup"><span data-stu-id="8aa63-118">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="8aa63-119">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="8aa63-119">Credential</span></span>| <span data-ttu-id="8aa63-120">Указывает учетные данные для запуска процесса.</span><span class="sxs-lookup"><span data-stu-id="8aa63-120">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="8aa63-121">Ensure</span><span class="sxs-lookup"><span data-stu-id="8aa63-121">Ensure</span></span>| <span data-ttu-id="8aa63-122">Указывает, существуют ли процессы.</span><span class="sxs-lookup"><span data-stu-id="8aa63-122">Specifies whether the processes exists.</span></span> <span data-ttu-id="8aa63-123">Если процесс существует, укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="8aa63-123">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="8aa63-124">В противном случае укажите значение Absent.</span><span class="sxs-lookup"><span data-stu-id="8aa63-124">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="8aa63-125">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="8aa63-125">The default is "Present".</span></span>|
| <span data-ttu-id="8aa63-126">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="8aa63-126">StandardErrorPath</span></span>| <span data-ttu-id="8aa63-127">Путь, по которому процессы записывают стандартную ошибку.</span><span class="sxs-lookup"><span data-stu-id="8aa63-127">The path to which the processes write standard error.</span></span> <span data-ttu-id="8aa63-128">Все существующие файлы в этом каталоге будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="8aa63-128">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="8aa63-129">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="8aa63-129">StandardInputPath</span></span>| <span data-ttu-id="8aa63-130">Поток, из которого процесс получает стандартные входные данные.</span><span class="sxs-lookup"><span data-stu-id="8aa63-130">The stream from which the process receives standard input.</span></span>|
| <span data-ttu-id="8aa63-131">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="8aa63-131">StandardOutputPath</span></span>| <span data-ttu-id="8aa63-132">Путь, по которому процессы записывают стандартные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="8aa63-132">The path of the file to which the processes write standard output.</span></span> <span data-ttu-id="8aa63-133">Все существующие файлы в этом каталоге будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="8aa63-133">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="8aa63-134">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="8aa63-134">WorkingDirectory</span></span>| <span data-ttu-id="8aa63-135">Расположение, которое используется в качестве текущего рабочего каталога для процессов.</span><span class="sxs-lookup"><span data-stu-id="8aa63-135">The location used as the current working directory for the processes.</span></span>|
| <span data-ttu-id="8aa63-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="8aa63-136">DependsOn</span></span> | <span data-ttu-id="8aa63-137">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="8aa63-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="8aa63-138">Например, если идентификатор первого запускаемого блока скрипта для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, синтаксис использования этого свойства будет таким: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="8aa63-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **_ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"` .</span></span>|
