---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Повторение задачи для нескольких объектов (ForEach-Object)
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 64d85edad4a6931b2376b95b6d1f5b4d5194399f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086176"
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a><span data-ttu-id="ead58-103">Повторение задачи для нескольких объектов (ForEach-Object)</span><span class="sxs-lookup"><span data-stu-id="ead58-103">Repeating a Task for Multiple Objects (ForEach-Object)</span></span>

<span data-ttu-id="ead58-104">Командлет **ForEach-Object** использует блоки скриптов и дескриптор `$_` текущего объекта конвейера, чтобы вы могли выполнить команду для каждого объекта в конвейере.</span><span class="sxs-lookup"><span data-stu-id="ead58-104">The **ForEach-Object** cmdlet uses script blocks and the `$_` descriptor for the current pipeline object to let you run a command on each object in the pipeline.</span></span> <span data-ttu-id="ead58-105">Это можно использовать для выполнения некоторых сложных задач.</span><span class="sxs-lookup"><span data-stu-id="ead58-105">This can be used to perform some complicated tasks.</span></span>

<span data-ttu-id="ead58-106">Одним из случаев, где это может пригодиться, является обработка данных, делающая их более полезными.</span><span class="sxs-lookup"><span data-stu-id="ead58-106">One situation where this can be useful is manipulating data to make it more useful.</span></span> <span data-ttu-id="ead58-107">Например, класс Win32_LogicalDisk из инструментария WMI можно использовать для возврата сведений о свободном пространстве на каждом локальном диске.</span><span class="sxs-lookup"><span data-stu-id="ead58-107">For example, the Win32_LogicalDisk class from WMI can be used to return free space information for each local disk.</span></span> <span data-ttu-id="ead58-108">Данные возвращаются в виде байтов, что затрудняет их восприятие:</span><span class="sxs-lookup"><span data-stu-id="ead58-108">The data is returned in terms of bytes, however, which makes it difficult to read:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

<span data-ttu-id="ead58-109">Можно преобразовать FreeSpace в мегабайты, дважды разделив каждое значение на 1024. После первого деления данные представлены в килобайтах, после второго — в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="ead58-109">We can convert the FreeSpace value to megabytes by dividing each value by 1024 twice; after the first division, the data is in kilobytes, and after the second division it is megabytes.</span></span> <span data-ttu-id="ead58-110">Это можно сделать в блоке сценария ForEach-Object, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="ead58-110">You can do that in a ForEach-Object script block by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

<span data-ttu-id="ead58-111">К сожалению, в результате получаются данные без соответствующей метки.</span><span class="sxs-lookup"><span data-stu-id="ead58-111">Unfortunately, the output is now data with no associated label.</span></span> <span data-ttu-id="ead58-112">Так как свойства инструментария WMI, такие как это, доступны только для чтения, непосредственное преобразование FreeSpace невозможно.</span><span class="sxs-lookup"><span data-stu-id="ead58-112">Because WMI properties such as this are read-only, you cannot directly convert FreeSpace.</span></span> <span data-ttu-id="ead58-113">Если ввести следующее:</span><span class="sxs-lookup"><span data-stu-id="ead58-113">If you type this:</span></span>

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="ead58-114">Отображается сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="ead58-114">You get an error message:</span></span>

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

<span data-ttu-id="ead58-115">Вы можете реорганизовать данные с помощью некоторых усовершенствованных методик, однако проще создать объект с помощью **Select-Object**.</span><span class="sxs-lookup"><span data-stu-id="ead58-115">You could reorganize the data by using some advanced techniques, but a simpler approach is to create a new object, by using **Select-Object**.</span></span>