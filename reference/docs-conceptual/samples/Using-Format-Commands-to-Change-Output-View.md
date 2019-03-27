---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Использование команд Format для изменения представления вывода
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 35ccd2525d40ffd5e3f25a1abfa38904a109bde5
ms.sourcegitcommit: 396509cd0d415acc306b68758b6f833406e26bf5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/21/2019
ms.locfileid: "58320427"
---
# <a name="using-format-commands-to-change-output-view"></a>Использование команд Format для изменения представления вывода

Windows PowerShell содержит набор командлетов, позволяющих пользователю контролировать, какие свойства должны отображаться для определенных объектов. Имена всех этих командлетов начинаются глаголом **Format**. Они позволяют выбрать для отображения одно или несколько свойств.

С глагола **Format** начинаются командлеты **Format-Wide**, **Format-List**, **Format-Table** и **Format-Custom**. В этом руководстве пользователя рассматриваются только командлеты **Format-Wide**, **Format-List** и **Format-Table**.

Каждый командлет форматирования имеет свойства по умолчанию, которые используются, если не задается отображение каких-либо определенных свойств. Для указания свойств, которые нужно отобразить, каждый командлет использует одно и то же имя параметра **Property**. Так как командлет **Format-Wide** отображает только одно свойство, для его параметра **Property** задается только одно значение, но в качестве значений параметров свойств у командлетов **Format-List** и **Format-Table** задается список имен свойств.

Если команда **Get-Process -Name powershell** используется во время работы двух экземпляров Windows PowerShell, формируются следующие выходные данные:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

Оставшаяся часть этого раздела посвящена ознакомлению с тем, как использовать командлеты **Format** для изменения способа отображения выходных данных команды.

### <a name="using-format-wide-for-single-item-output"></a>Применение командлета Format-Wide для вывода с одним элементом

По умолчанию командлет **Format-Wide** отображает только свойство по умолчанию для объекта. Данные, связанные с каждым объектом, отображаются в одном столбце:

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

Можно также задать свойство, отличное от используемого по умолчанию:

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a>Настройка отображения командлета Format-Wide с помощью параметра Column

С помощью командлета `Format-Wide` одновременно можно отобразить только одно свойство.
Это может быть полезным при отображении простых списков, у которых в каждой строке отображается только один элемент.
Для получения простого списка нужно установить для параметра **Column** значение 1, введя следующее:

```powershell
Get-Command -Verb Format | Format-Wide -Property Noun -Column 1
```

```output
Custom
Hex
List
Table
Wide
```

### <a name="using-format-list-for-a-list-view"></a>Использование командлета Format-List для представления в виде списка

Командлет **Format-List** показывает объект в виде списка, в котором каждое свойство имеет метку и отображается в отдельной строке:

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

Можно указать произвольное число свойств:

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a>Получение подробных сведений с помощью подстановочных знаков в командлете Format-List

Командлет **Format-List** позволяет использовать подстановочные знаки в качестве значения параметра **Property**. Это дает возможность отображать подробные сведения. Часто объекты содержат больше информации, чем необходимо. Поэтому Windows PowerShell по умолчанию выводит значения не всех свойств. Чтобы вывести список всех свойств объекта, используйте команду **Format-List -Property \&#42;**. Следующая команда формирует более 60 строк выходных данных для одного процесса:

```powershell
Get-Process -Name powershell | Format-List -Property *
```

Хотя команда **Format-List** и полезна для вывода подробных сведений, для получения сведений, содержащих много элементов, обычно удобнее использовать упрощенное табличное представление.

### <a name="using-format-table-for-tabular-output"></a>Применение командлета Format-Table для табличного вывода

Если использовать командлет **Format-Table** без указания имен свойств для форматирования вывода команды **Get-Process**, будут получены точно такие же выходные данные, что и без использования форматирования. Это вызвано тем, что процессы обычно показываются в виде таблицы, как и большинство объектов Windows PowerShell.

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a>Улучшение вывода командлета Format-Table (параметр AutoSize)

Хотя табличное представление и полезно при выводе большого количества сведений для сравнения, интерпретация данных может вызвать затруднения, если экран слишком узок и не вмещает все данные. Например, если отобразить путь процесса, идентификатор, имя и организацию, данные в столбцах пути процесса и организации окажутся обрезанными:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

Если указать параметр **AutoSize** при выполнении команды **Format-Table**, Windows PowerShell вычислит ширину столбцов по ширине реально отображаемых данных. Это улучшит внешний вид столбца **Path**, но значение столбца с названием организации останется обрезанным:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

Командлет **Format-Table** может обрезать данные, но это происходит только на правой границе экрана. Свойствам, за исключением последнего отображаемого, выделяется столько места, сколько нужно для корректного вывода самого длинного элемента данных. Если поменять местами элементы **Path** и **Company** в списке значений **Property**, название организации отображается полностью, но путь обрезан:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

Команда **Format-Table** предполагает, что чем ближе свойство к началу списка свойств, тем оно важнее. В связи с этим предпринимается попытка отобразить полностью свойства, находящиеся ближе всего к началу. Если команда **Format-Table** не может отобразить все свойства, она удаляет некоторые столбцы из выходных данных и выдает предупреждение. Такое поведение можно наблюдать, если поместить свойство **Name** в конец списка:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

В приведенных выше входных данных столбец идентификатора обрезан, чтобы его значение уместилось в списке, а заголовки столбцов расположены вертикально. Автоматическое изменение размера столбцов не всегда дает желаемый результат.

#### <a name="wrapping-format-table-output-in-columns-wrap"></a>Перенос на следующую строку вывода командлета Format-Table в столбцах (параметр Wrap)

Длинные данные командлета **Format-Table** можно принудительно перенести на следующую строку в пределах столбца с помощью параметра **Wrap**. Использование параметра **Wrap** в отдельности не всегда приводит к ожидаемому результату, так как если не указан еще и параметр **AutoSize**, применяются параметры по умолчанию:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

Преимущество использования параметра **Wrap** без других параметров заключается в отсутствии существенного замедления обработки. Использование параметра **AutoSize** во время выполнения рекурсивного вывода списка файлов в большом каталоге может потребовать значительного объема памяти и времени перед отображением первых выходных данных.

Если загрузка системы не имеет решающего значения, параметр **AutoSize** хорошо работает в сочетании с параметром **Wrap**. Начальным столбцам всегда выделяется необходимый размер для вывода элементов в одной строке, как и при указании параметра **AutoSize** без параметра **Wrap**. Единственное отличие состоит в том, что последний столбец будет при необходимости перенесен на следующую строку:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

Некоторые столбцы могут не быть показаны, если первым указать самый широкий столбец, поэтому безопаснее указывать первыми самые маленькие элементы данных. В следующем примере первым указан чрезвычайно большой элемент — путь. Даже при переносе на следующую строку последний столбец **Name** теряется:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a>Организация табличного вывода (параметр -GroupBy)

Другим полезным параметром управления табличным выводом является **GroupBy**. Длинные табличные списки особенно тяжелы для сравнения. Параметр **GroupBy** группирует выходные данные в соответствии со значением свойства. Например, можно сгруппировать процессы по организации для упрощения проверки, исключая название организации из списка свойства:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```