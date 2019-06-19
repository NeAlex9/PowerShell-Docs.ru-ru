---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Работа с файлами и папками
ms.openlocfilehash: 0f7cb233918b59475417ec49b611ecc25a94ebe1
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030684"
---
# <a name="working-with-files-and-folders"></a><span data-ttu-id="158de-103">Работа с файлами и папками</span><span class="sxs-lookup"><span data-stu-id="158de-103">Working with Files and Folders</span></span>

<span data-ttu-id="158de-104">Просмотр содержимого дисков Windows PowerShell и управление хранящимися на них элементами аналогично управлению файлами и папками на физических дисках Windows.</span><span class="sxs-lookup"><span data-stu-id="158de-104">Navigating through Windows PowerShell drives and manipulating the items on them is similar to manipulating files and folders on Windows physical disk drives.</span></span> <span data-ttu-id="158de-105">В этом разделе мы обсудим выполнение конкретных задач по управлению файлами и папками с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="158de-105">This section discusses how to deal with specific file and folder manipulation tasks using PowerShell.</span></span>

## <a name="listing-all-the-files-and-folders-within-a-folder"></a><span data-ttu-id="158de-106">Получение списка файлов и папок, содержащихся в папке</span><span class="sxs-lookup"><span data-stu-id="158de-106">Listing All the Files and Folders Within a Folder</span></span>

<span data-ttu-id="158de-107">Извлечь все элементы непосредственно из папки можно с помощью командлета **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="158de-107">You can get all items directly within a folder by using **Get-ChildItem**.</span></span> <span data-ttu-id="158de-108">Для отображения скрытых и системных элементов добавьте необязательный параметр **Force**.</span><span class="sxs-lookup"><span data-stu-id="158de-108">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="158de-109">Например, эта команда отображает непосредственное содержимое диска C Windows PowerShell (которое совпадает с содержимым физического диска C Windows):</span><span class="sxs-lookup"><span data-stu-id="158de-109">For example, this command displays the direct contents of Windows PowerShell Drive C (which is the same as the Windows physical drive C):</span></span>

```powershell
Get-ChildItem -Path C:\ -Force
```

<span data-ttu-id="158de-110">Эта команда выводит только элементы, содержащиеся на диске непосредственно, так же как и команда **DIR** оболочки Cmd.exe или команда **ls** оболочки UNIX.</span><span class="sxs-lookup"><span data-stu-id="158de-110">The command lists only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="158de-111">Для показа вложенных элементов необходимо также указать параметр **-Recurse**.</span><span class="sxs-lookup"><span data-stu-id="158de-111">In order to show contained items, you need to specify the **-Recurse** parameter as well.</span></span> <span data-ttu-id="158de-112">(Время выполнения этой операции будет очень велико.) Для вывода всего содержимого диска C введите:</span><span class="sxs-lookup"><span data-stu-id="158de-112">(This can take an extremely long time to complete.) To list everything on the C drive:</span></span>

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

<span data-ttu-id="158de-113">Командлет **Get-ChildItem** позволяет отфильтровать элементы с помощью параметров **Path**, **Filter**, **Include** и **Exclude**, но обычно осуществляется лишь фильтрация по имени.</span><span class="sxs-lookup"><span data-stu-id="158de-113">**Get-ChildItem** can filter items with its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those are typically based only on name.</span></span> <span data-ttu-id="158de-114">Сложную фильтрацию на основе других свойств элементов можно выполнить с помощью командлета **Where-Object**.</span><span class="sxs-lookup"><span data-stu-id="158de-114">You can perform complex filtering based on other properties of items by using **Where-Object**.</span></span>

<span data-ttu-id="158de-115">Следующая команда находит все исполняемые файлы в папке Program Files, которые были в последний раз изменены после 1 октября 2005 г. и размер которых не менее одного мегабайта и не более десяти мегабайт:</span><span class="sxs-lookup"><span data-stu-id="158de-115">The following command finds all executables within the Program Files folder that were last modified after October 1, 2005 and which are neither smaller than 1 megabyte nor larger than 10 megabytes:</span></span>

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

## <a name="copying-files-and-folders"></a><span data-ttu-id="158de-116">Копирование файлов и папок</span><span class="sxs-lookup"><span data-stu-id="158de-116">Copying Files and Folders</span></span>

<span data-ttu-id="158de-117">Копирование выполняется с помощью командлета **Copy-Item**.</span><span class="sxs-lookup"><span data-stu-id="158de-117">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="158de-118">Следующая команда создает резервную копию C:\\boot.ini в C:\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="158de-118">The following command backs up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

<span data-ttu-id="158de-119">Если целевой файл уже существует, то попытка копирования завершается неудачей.</span><span class="sxs-lookup"><span data-stu-id="158de-119">If the destination file already exists, the copy attempt fails.</span></span> <span data-ttu-id="158de-120">Чтобы перезаписать имеющийся целевой файл, используйте параметр **Force**.</span><span class="sxs-lookup"><span data-stu-id="158de-120">To overwrite a pre-existing destination, use the **Force** parameter:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

<span data-ttu-id="158de-121">Эта команда работает, даже если целевой объект доступен только для чтения.</span><span class="sxs-lookup"><span data-stu-id="158de-121">This command works even when the destination is read-only.</span></span>

<span data-ttu-id="158de-122">Так же выполняется и копирование папок.</span><span class="sxs-lookup"><span data-stu-id="158de-122">Folder copying works the same way.</span></span> <span data-ttu-id="158de-123">Эта команда рекурсивно копирует папку "C:\\temp\\test1" в новую папку "c:\\temp\\DeleteMe".</span><span class="sxs-lookup"><span data-stu-id="158de-123">This command copies the folder C:\\temp\\test1 to the new folder C:\\temp\\DeleteMe recursively:</span></span>

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

<span data-ttu-id="158de-124">Можно также скопировать избранные элементы.</span><span class="sxs-lookup"><span data-stu-id="158de-124">You can also copy a selection of items.</span></span> <span data-ttu-id="158de-125">Следующая команда копирует все файлы .txt, содержащиеся в папке "c:\\data", в папку "c:\\temp\\text":</span><span class="sxs-lookup"><span data-stu-id="158de-125">The following command copies all .txt files contained anywhere in c:\\data to c:\\temp\\text:</span></span>

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

<span data-ttu-id="158de-126">Для копирования элементов файловой системы можно использовать и другие средства.</span><span class="sxs-lookup"><span data-stu-id="158de-126">You can still use other tools to perform file system copies.</span></span> <span data-ttu-id="158de-127">В Windows PowerShell по-прежнему работают команды XCOPY, ROBOCOPY и такие COM-объекты, как **Scripting.FileSystemObject**.</span><span class="sxs-lookup"><span data-stu-id="158de-127">XCOPY, ROBOCOPY, and COM objects, such as the **Scripting.FileSystemObject,** all work in Windows PowerShell.</span></span> <span data-ttu-id="158de-128">Например, можно воспользоваться COM-классом **Scripting.FileSystem** сервера сценариев Windows для создания резервной копии файла C:\\boot.ini в файле C:\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="158de-128">For example, you can use the Windows Script Host **Scripting.FileSystem COM** class to back up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

## <a name="creating-files-and-folders"></a><span data-ttu-id="158de-129">Создание файлов и папок</span><span class="sxs-lookup"><span data-stu-id="158de-129">Creating Files and Folders</span></span>

<span data-ttu-id="158de-130">Создание новых элементов осуществляется одинаковым образом всеми поставщиками Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="158de-130">Creating new items works the same on all Windows PowerShell providers.</span></span> <span data-ttu-id="158de-131">Если поставщик Windows PowerShell поддерживает более одного типа элементов (например, поставщик Windows PowerShell FileSystem различает каталоги и файлы), необходимо указать тип элемента.</span><span class="sxs-lookup"><span data-stu-id="158de-131">If a Windows PowerShell provider has more than one type of item—for example, the FileSystem Windows PowerShell provider distinguishes between directories and files—you need to specify the item type.</span></span>

<span data-ttu-id="158de-132">Эта команда создает папку "C:\\temp\\New Folder":</span><span class="sxs-lookup"><span data-stu-id="158de-132">This command creates a new folder C:\\temp\\New Folder:</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

<span data-ttu-id="158de-133">Эта команда создает пустой файл "C:\\temp\\New Folder\\file.txt":</span><span class="sxs-lookup"><span data-stu-id="158de-133">This command creates a new empty file C:\\temp\\New Folder\\file.txt</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

## <a name="removing-all-files-and-folders-within-a-folder"></a><span data-ttu-id="158de-134">Удаление всех файлов и папок, содержащихся в папке</span><span class="sxs-lookup"><span data-stu-id="158de-134">Removing All Files and Folders Within a Folder</span></span>

<span data-ttu-id="158de-135">Удалить вложенные элементы можно с помощью командлета **Remove-Item**, однако он потребует подтверждения удаления, если элемент сам что-нибудь содержит.</span><span class="sxs-lookup"><span data-stu-id="158de-135">You can remove contained items using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="158de-136">Например, при попытке удаления папки C:\\temp\\DeleteMe, которая содержит другие элементы, Windows PowerShell предварительно предложит подтвердить удаление этой папки:</span><span class="sxs-lookup"><span data-stu-id="158de-136">For example, if you attempt to delete the folder C:\\temp\\DeleteMe that contains other items, Windows PowerShell prompts you for confirmation before deleting the folder:</span></span>

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="158de-137">Если подтверждение для каждого вложенного элемента нежелательно, задайте параметр **Recurse**:</span><span class="sxs-lookup"><span data-stu-id="158de-137">If you do not want to be prompted for each contained item, specify the **Recurse** parameter:</span></span>

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

## <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a><span data-ttu-id="158de-138">Отображение локальной папки в виде диска, доступного в Windows</span><span class="sxs-lookup"><span data-stu-id="158de-138">Mapping a Local Folder as a Windows Accessible Drive</span></span>

<span data-ttu-id="158de-139">Отобразить локальную папку можно с помощью команды **subst**.</span><span class="sxs-lookup"><span data-stu-id="158de-139">You can also map a local folder, using the **subst** command.</span></span> <span data-ttu-id="158de-140">Следующая команда создает локальный диск P:, корневым каталогом которого является локальный каталог Program Files:</span><span class="sxs-lookup"><span data-stu-id="158de-140">The following command creates a local drive P: rooted in the local Program Files directory:</span></span>

```powershell
subst p: $env:programfiles
```

<span data-ttu-id="158de-141">Как и в случае сетевых дисков, диски, отображенные в оболочке Windows PowerShell с помощью команды **subst**, немедленно становятся доступными оболочке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="158de-141">Just as with network drives, drives mapped within Windows PowerShell using **subst** are immediately visible to the Windows PowerShell shell.</span></span>

## <a name="reading-a-text-file-into-an-array"></a><span data-ttu-id="158de-142">Чтение текстового файла в массив</span><span class="sxs-lookup"><span data-stu-id="158de-142">Reading a Text File into an Array</span></span>

<span data-ttu-id="158de-143">Одним из наиболее общих форматов хранения текстовых данных является файл, отдельные строки которого рассматриваются как отдельные элементы.</span><span class="sxs-lookup"><span data-stu-id="158de-143">One of the more common storage formats for text data is in a file with separate lines treated as distinct data elements.</span></span> <span data-ttu-id="158de-144">Командлет **Get-Content** используется для чтения всего файла за один шаг, как показано далее.</span><span class="sxs-lookup"><span data-stu-id="158de-144">The **Get-Content** cmdlet can be used to read an entire file in one step, as shown here:</span></span>

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional
with Data Execution Prevention" /noexecute=optin /fastdetect
```

<span data-ttu-id="158de-145">Командлет **Get-Content** сразу рассматривает данные, считанные из файла, как массив с одним элементом на строку содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="158de-145">**Get-Content** already treats the data read from the file as an array, with one element per line of file content.</span></span> <span data-ttu-id="158de-146">Убедиться в этом можно, проверив свойство **Length** полученного содержимого:</span><span class="sxs-lookup"><span data-stu-id="158de-146">You can confirm this by checking the **Length** of the returned content:</span></span>

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

<span data-ttu-id="158de-147">Эта команда наиболее полезна для непосредственного ввода в Windows PowerShell информационных списков.</span><span class="sxs-lookup"><span data-stu-id="158de-147">This command is most useful for getting lists of information into Windows PowerShell directly.</span></span> <span data-ttu-id="158de-148">Например, можно хранить в файле "C:\\temp\\domainMembers.txt" список имен компьютеров или IP-адресов по одному имени на каждую строку файла.</span><span class="sxs-lookup"><span data-stu-id="158de-148">For example, you might store a list of computer names or IP addresses in a file C:\\temp\\domainMembers.txt, with one name on each line of the file.</span></span> <span data-ttu-id="158de-149">Можно использовать командлет **Get-Content**, чтобы извлечь содержимое файла и поместить его в переменную **$Computers**:</span><span class="sxs-lookup"><span data-stu-id="158de-149">You can use **Get-Content** to retrieve the file contents and put them in the variable **$Computers**:</span></span>

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

<span data-ttu-id="158de-150">Теперь переменная **$Computers** представляет собой массив, содержащий в каждом элементе имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="158de-150">**$Computers** is now an array containing a computer name in each element.</span></span>
