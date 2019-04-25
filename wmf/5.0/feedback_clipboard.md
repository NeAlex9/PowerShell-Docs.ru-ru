---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: d5ec95abb1d3160afc4179cff991cb5ef72d85fe
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057304"
---
# <a name="clipboard-cmdlets"></a><span data-ttu-id="59f74-102">Командлеты Clipboard</span><span class="sxs-lookup"><span data-stu-id="59f74-102">Clipboard cmdlets</span></span>
<span data-ttu-id="59f74-103">Командлеты**Get-Clipboard** и **Set-Clipboard** упрощают передачу содержимого в сеанс Windows PowerShell и из него.</span><span class="sxs-lookup"><span data-stu-id="59f74-103">**Get-Clipboard** and **Set-Clipboard** make it easier for you to transfer content to and from a Windows PowerShell session.</span></span> <span data-ttu-id="59f74-104">Например, если скопировать три файла с помощью проводника Windows в буфер обмена (скажем, выбрав их и нажав клавишу `ctrl-c`), можно затем легко получить содержимое буфера обмена в виде списка файлов:</span><span class="sxs-lookup"><span data-stu-id="59f74-104">For example, if you use Windows Explorer to copy three files to the clipboard (by selecting them and pressing `ctrl-c`, for example), you can then easily access the contents of the clipboard as a list of files:</span></span>

```powershell
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


<span data-ttu-id="59f74-105">Командлеты Clipboard поддерживают изображения, звуковые файлы, списки файлов и текст.</span><span class="sxs-lookup"><span data-stu-id="59f74-105">The Clipboard cmdlets support images, audio files, file lists, and text.</span></span>
