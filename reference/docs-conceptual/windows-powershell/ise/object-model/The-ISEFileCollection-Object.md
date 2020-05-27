---
ms.date: 12/31/2019
keywords: powershell,командлет
title: Объект ISEFileCollection
ms.openlocfilehash: 4192afa9dc91d9ea4c4c084d3ba0175483620229
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809340"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="77e5b-103">Объект ISEFileCollection</span><span class="sxs-lookup"><span data-stu-id="77e5b-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="77e5b-104">Объект **ISEFileCollection**  — это коллекция объектов **ISEFile**.</span><span class="sxs-lookup"><span data-stu-id="77e5b-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="77e5b-105">Примером является коллекция `$psISE.CurrentPowerShellTab.Files`.</span><span class="sxs-lookup"><span data-stu-id="77e5b-105">An example is the `$psISE.CurrentPowerShellTab.Files` collection.</span></span>

## <a name="methods"></a><span data-ttu-id="77e5b-106">Методы</span><span class="sxs-lookup"><span data-stu-id="77e5b-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="77e5b-107">Add\( \[FullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="77e5b-107">Add\( \[FullPath\] \)</span></span>

<span data-ttu-id="77e5b-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="77e5b-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="77e5b-109">Создает и возвращает новый файл без имени и добавляет его в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="77e5b-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="77e5b-110">Свойство **IsUntitled** созданного файла имеет значение `$true`.</span><span class="sxs-lookup"><span data-stu-id="77e5b-110">The **IsUntitled** property of the newly created file is `$true`.</span></span>

<span data-ttu-id="77e5b-111">**\[FullPath\]**  — необязательная строка. Полный путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="77e5b-111">**\[FullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="77e5b-112">Исключение возникает, если включен параметр **FullPath** и относительный путь или если вместо полного пути используется имя файла.</span><span class="sxs-lookup"><span data-stu-id="77e5b-112">An exception is generated if you include the **FullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="77e5b-113">Remove\( File, \[Force\] \)</span><span class="sxs-lookup"><span data-stu-id="77e5b-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="77e5b-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="77e5b-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="77e5b-115">Удаляет указанный файл из текущей вкладки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77e5b-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="77e5b-116">**File** — строка. Файл ISEFile, удаляемый из коллекции.</span><span class="sxs-lookup"><span data-stu-id="77e5b-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="77e5b-117">Если файл не был сохранен, этот метод создает исключение.</span><span class="sxs-lookup"><span data-stu-id="77e5b-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="77e5b-118">Используйте параметр **Force** для принудительного удаления несохраненного файла.</span><span class="sxs-lookup"><span data-stu-id="77e5b-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="77e5b-119">**\[Force\]**  — необязательное логическое значение. Если задано значение `$true`, предоставляет разрешение на удаление файла, даже если он не был сохранен с момента последнего использования.</span><span class="sxs-lookup"><span data-stu-id="77e5b-119">**\[Force\]** - optional Boolean If set to `$true`, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="77e5b-120">Значение по умолчанию — `$false`.</span><span class="sxs-lookup"><span data-stu-id="77e5b-120">The default is `$false`.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="77e5b-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="77e5b-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="77e5b-122">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="77e5b-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="77e5b-123">Выбирает файл, который задается параметром **SelectedFile**.</span><span class="sxs-lookup"><span data-stu-id="77e5b-123">Selects the file that is specified by the **SelectedFile** parameter.</span></span>

<span data-ttu-id="77e5b-124">**SelectedFile** — Microsoft.PowerShell.Host.ISE.ISEFile. Выбираемый файл ISEFile.</span><span class="sxs-lookup"><span data-stu-id="77e5b-124">**SelectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="77e5b-125">См. также:</span><span class="sxs-lookup"><span data-stu-id="77e5b-125">See Also</span></span>

- [<span data-ttu-id="77e5b-126">Объект ISEFile</span><span class="sxs-lookup"><span data-stu-id="77e5b-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="77e5b-127">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="77e5b-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="77e5b-128">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="77e5b-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
