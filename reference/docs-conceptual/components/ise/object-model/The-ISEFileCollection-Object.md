---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект ISEFileCollection
ms.openlocfilehash: 96db51ee921cc0fa34803091d563bc6e118643b6
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030517"
---
# <a name="the-isefilecollection-object"></a>Объект ISEFileCollection

Объект **ISEFileCollection**  — это коллекция объектов **ISEFile**. Примером является коллекция $psISE.CurrentPowerShellTab.Files.

## <a name="methods"></a>Методы

### <a name="add-fullpath-"></a>Add\( \[fullPath\] \)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Создает и возвращает новый файл без имени и добавляет его в коллекцию. Свойство **IsUntitled** созданного файла имеет значение **$true**.

**\[fullPath\]**  — необязательная строка. Полный путь к файлу. Исключение возникает, если включен параметр **fullPath** и относительный путь или если вместо полного пути используется имя файла.

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a>Remove\( File, \[Force\] \)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Удаляет указанный файл из текущей вкладки PowerShell.

**File** — строка. Файл ISEFile, удаляемый из коллекции. Если файл не был сохранен, этот метод создает исключение. Используйте параметр **Force** для принудительного удаления несохраненного файла.

**\[Force\]**  — необязательное логическое значение. Если задано значение **$true**, предоставляет разрешение на удаление файла, даже если он не был сохранен с момента последнего использования. Значение по умолчанию — **$false**.

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a>SetSelectedFile\( selectedFile \)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Выбирает файл, который задается параметром **selectedFile**.

**selectedFile** — Microsoft.PowerShell.Host.ISE.ISEFile. Выбираемый файл ISEFile.

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a>См. также

- [Объект ISEFile](The-ISEFile-Object.md)
- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)
