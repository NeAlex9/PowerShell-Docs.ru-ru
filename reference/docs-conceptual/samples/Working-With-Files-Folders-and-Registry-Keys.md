---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Работа с файлами, папками и разделами реестра
ms.openlocfilehash: 0c8716c384827d0816e2847ff81232c14638681b
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030761"
---
# <a name="working-with-files-folders-and-registry-keys"></a>Работа с файлами, папками и разделами реестра

Windows PowerShell использует существительное **Item**, чтобы ссылаться на элементы, найденные на диске Windows PowerShell. При работе с поставщиком FileSystem Windows PowerShell **Item** может быть файлом, папкой или диском Windows PowerShell. Создание списков элементов и работа с ними является критически важной задачей в большинстве административных учреждений, поэтому необходимо подробно обсудить ее.

## <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a>Перечисление файлов, папок и разделов реестра (Get-ChildItem)

Так как получение коллекции элементов из определенного расположения является обычной задачей, командлет **Get-ChildItem** разработан специально для возврата всех элементов, найденных в контейнере, например в папке.

Если необходимо вернуть все файлы и папки, которые находятся непосредственно в папке C:\\Windows, введите:

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

Списки выглядят аналогично тем спискам, которые появляются при вводе команды **dir** в **Cmd.exe** или команды **ls** в командной оболочке UNIX.

С помощью параметров командлета **Get-ChildItem** можно создавать очень сложные списки. Далее рассмотрим несколько сценариев. Синтаксис командлета **Get-ChildItem** можно увидеть, введя:

```powershell
Get-Command -Name Get-ChildItem -Syntax
```

Эти параметры можно скомбинировать и сопоставить для получения настраиваемых выходных данных.

### <a name="listing-all-contained-items--recurse"></a>Перечисление всех элементов в контейнере (-Recurse)

Чтобы увидеть оба элемента в папке Windows и все элементы во вложенных папках, используйте параметр **Recurse** для **Get-ChildItem**. В списке отображается все, что находится в папке Windows, а также элементы в ее вложенных папках. Например:

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

### <a name="filtering-items-by-name--name"></a>Фильтрация элементов по имени (-Name)

Чтобы отобразить только имена элементов, используйте параметр **Name** для **Get-Childitem**:

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

### <a name="forcibly-listing-hidden-items--force"></a>Принудительное перечисление скрытых элементов (-Force)

В выходных данных команды **Get-ChildItem** не отображаются элементы, которые обычно невидимы в проводнике или Cmd.exe. Чтобы показать скрытые элементы, используйте параметр **Force** для **Get-ChildItem**. Например:

```powershell
Get-ChildItem -Path C:\Windows -Force
```

Этот параметр называется Force, так как позволяет принудительно переопределить обычное поведение команды **Get-ChildItem**. Параметр Force широко используется для принудительного выполнения действия командлетом. Тем не менее, он не будет выполнять действия, компрометирующие систему безопасности.

### <a name="matching-item-names-with-wildcards"></a>Сопоставление имен элементов с подстановочными знаками

Команда **Get-ChildItem** допускает подстановочные знаки в пути к перечисляемым элементам.

Так как сопоставление с подстановочными знаками обрабатывается подсистемой Windows PowerShell, все командлеты, которые принимают подстановочные знаки, используют одну нотацию и имеют одно поведение сопоставления. В нотацию подстановочных знаков Windows PowerShell входит:

- Звездочка (\*) — соответствует нулю или большему количеству вхождений любого символа.

- знак вопроса (?) — соответствует ровно одному символу;

- Открывающая квадратная скобка (\[) и закрывающая квадратная скобка (]) — заключают в себя набор символов для сопоставления.

Далее приводится несколько примеров работы спецификации из подстановочных знаков.

Чтобы найти в каталоге Windows все файлы, имеющие суффикс **.log** и ровно пять символов в основном имени, введите следующую команду:

```
PS> Get-ChildItem -Path C:\Windows\?????.log

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

Чтобы найти в каталоге Windows все файлы с именами, начинающимися на букву **x**, введите:

```powershell
Get-ChildItem -Path C:\Windows\x*
```

Чтобы найти все файлы с именами, начинающимися на **x** или **z**, введите:

```powershell
Get-ChildItem -Path C:\Windows\[xz]*
```

### <a name="excluding-items--exclude"></a>Исключение элементов (-Exclude)

Вы можете исключить определенные элементы с помощью параметра **Exclude** для Get-ChildItem. Это позволит вам выполнить сложную фильтрацию в одном операторе.

Например, предположим, что вы пытаетесь найти библиотеку службы времени Windows в папке System32 и все, что вам известно об имени библиотеки, — то, что оно начинается на W и содержит "32".

Выражение **w\&#42;32\&#42;.dll** найдет все библиотеки DLL, удовлетворяющие условию, но может также вернуть библиотеки Windows 95 и библиотеки, совместимые с 16-разрядной версией Windows, в именах которых содержится "95" или "16". Файлы с такими числами в именах можно пропустить, используя параметр **Exclude** с шаблоном **\&#42;\[9516]\&#42;** :

```
PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude *[9516]*

Directory: Microsoft.PowerShell.Core\FileSystem::C:\WINDOWS\System32
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     174592 w32time.dll
-a---        2004-08-04   8:00 AM      22016 w32topl.dll
-a---        2004-08-04   8:00 AM     101888 win32spl.dll
-a---        2004-08-04   8:00 AM     172032 wldap32.dll
-a---        2004-08-04   8:00 AM     264192 wow32.dll
-a---        2004-08-04   8:00 AM      82944 ws2_32.dll
-a---        2004-08-04   8:00 AM      42496 wsnmp32.dll
-a---        2004-08-04   8:00 AM      22528 wsock32.dll
-a---        2004-08-04   8:00 AM      18432 wtsapi32.dll
```

### <a name="mixing-get-childitem-parameters"></a>Смешение параметров Get-ChildItem

В одной команде можно использовать несколько параметров **Get-ChildItem**. Перед тем как комбинировать параметры, убедитесь, что понимаете принципы сопоставления подстановочных знаков. Например, следующая команда не возвращает результатов:

```powershell
Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

Результаты отсутствуют, даже если существуют две библиотеки, которые начинаются на букву z в папке Windows.

Результаты не возвращены, так как подстановочный знак указан как часть пути. Хотя команда и была рекурсивной, командлет **Get-ChildItem** ограничил элементы до тех, которые находятся в папке Windows с именами, заканчивающимися на .dll.

Чтобы указать рекурсивный поиск для файлов, имена которых соответствуют специальному шаблону, используйте параметр **-Include**.

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```
