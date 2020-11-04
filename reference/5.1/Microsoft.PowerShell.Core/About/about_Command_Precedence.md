---
description: Описывает, как PowerShell определяет, какую команду выполнить.
keywords: powershell,командлет
ms.date: 02/13/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_command_precedence?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Command_Precedence
ms.openlocfilehash: 288c01af2d66aca786cf1b97ad844dd91cac45ca
ms.sourcegitcommit: f874dc1d4236e06a3df195d179f59e0a7d9f8436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "93232069"
---
# <a name="about-command-precedence"></a>О приоритете команд

## <a name="short-description"></a>Краткое описание
Описывает, как PowerShell определяет, какую команду выполнить.

## <a name="long-description"></a>Подробное описание

Очередность команд. описывает, как PowerShell определяет, какую команду запускать, если сеанс содержит несколько команд с одним и тем же именем. Команды в сеансе могут быть скрыты или заменены командами с тем же именем. В этой статье показано, как выполнить скрытые команды и избежать конфликтов имен команд.

## <a name="command-precedence"></a>Очередность команд

Если сеанс PowerShell содержит несколько команд с одинаковыми именами, то PowerShell определяет, какую команду выполнить, используя следующие правила.

Если указать путь к команде, PowerShell выполняет команду в расположении, указанном в пути.

Например, следующая команда запускает скрипт FindDocs.ps1 в каталоге C: \\ течдокс:

```
C:\TechDocs\FindDocs.ps1
```

В качестве функции безопасности PowerShell не выполняет исполняемые (собственные) команды, включая сценарии PowerShell, если команда не находится в пути, указанном в переменной среды PATH, `$env:path` или если не указан путь к файлу скрипта.

Чтобы выполнить скрипт, накоторый находится в текущем каталоге, укажите полный путь или введите точку, `.\` представляющую текущий каталог.

Например, чтобы запустить файл FindDocs.ps1 в текущем каталоге, введите:

```
.\FindDocs.ps1
```

### <a name="using-wildcards-in-execution"></a>Использование подстановочных знаков при выполнении

При выполнении команды можно использовать подстановочные знаки. Использование подстановочных знаков также называется *глобализации*.

PowerShell выполняет файл с подстановочным знаком, перед совпадением литерала.

Например, рассмотрим каталог со следующими файлами:

```
Get-ChildItem C:\temp\test


    Directory: C:\temp\test


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        5/20/2019   2:29 PM             28 a.ps1
-a----        5/20/2019   2:29 PM             28 [a1].ps1
```

Оба файла скрипта имеют одинаковое содержимое: `$MyInvocation.MyCommand.Path` .
Эта команда отображает имя вызываемого скрипта.

При запуске `[a1].ps1` файл `a.ps1` выполняется, даже если он `[a1].ps1` совпадает с литералом.

```powershell
C:\temp\test\[a1].ps1
```

```Output
C:\temp\test\a.ps1
```

Теперь попробуем удалить `a.ps1` файл и попытаться запустить его снова.

```powershell
Remove-Item C:\temp\test\a.ps1
C:\temp\test\[a1].ps1
```

```Output
C:\temp\test\[a1].ps1
```

Из выходных данных, которые выполняются в данный момент, можно увидеть, что `[a1].ps1` литеральное совпадение является единственным файлом, соответствующим шаблону шаблона.

Дополнительные сведения об использовании подстановочных знаков в PowerShell см. в разделе [about_Wildcards](about_Wildcards.md).

> [!NOTE]
> Чтобы ограничить поиск относительным путем, необходимо добавить перед именем скрипта `.\` путь. Это ограничивает поиск команд файлами по этому относительному пути. Без этого префикса другой синтаксис PowerShell может конфликтовать, и существует несколько гарантий, что файл будет найден.

Если путь не указан, PowerShell использует следующий порядок очередности при выполнении команд для всех элементов, загруженных в текущем сеансе:

  1. Псевдоним
  2. Компонент
  3. Командлет
  4. Внешние исполняемые файлы (программы и сценарии, не связанные с PowerShell)

Поэтому, если ввести "Help", PowerShell сначала ищет псевдоним с именем `help` , затем функцию с именем `Help` и, наконец, командлет с именем `Help` . Он запускает первый `help` найденный элемент.

Например, если сеанс содержит командлет и функцию с именем, то `Get-Map` при вводе `Get-Map` PowerShell выполняет функцию.

> [!NOTE]
> Это относится только к загруженным командам. При наличии `build` исполняемого файла и псевдонима `build` для функции с именем `Invoke-Build` внутри модуля, который не был загружен в текущий сеанс, PowerShell запускает `build` исполняемый файл. Он не выполняет автоматическую загрузку модулей, если в данном случае обнаруживает внешний исполняемый файл. Это происходит только в том случае, если не найдены внешние исполняемые файлы, которые вызываются псевдонимом, функцией или командлетом с заданным именем. Таким образом запускается автоматическая загрузка модуля.

Если в сеансе содержатся элементы одного типа с одинаковым именем, PowerShell запускает новый элемент.

Например, при импорте другого `Get-Date` командлета из модуля при вводе `Get-Date` PowerShell выполняет импортированную версию по собственному каналу.

## <a name="hidden-and-replaced-items"></a>Скрытые и замененные элементы

В результате этих правил элементы могут быть заменены или скрыты элементами с одинаковыми именами.

Элементы скрыты или затенены, если доступ к исходному элементу по-прежнему возможен, например, с помощью имени модуля или оснастки.

Например, при импорте функции, которая имеет то же имя, что и командлет в сеансе, этот командлет скрыт (но не заменяется), так как он был импортирован из оснастки или модуля.

Элементы заменяются или перезаписываются, если доступ к исходному элементу больше невозможен.

Например, при импорте переменной, имя которой совпадает с именем переменной в сеансе, исходная переменная заменяется и становится недоступной.
Нельзя определить переменную с именем модуля.

Кроме того, если ввести функцию в командной строке и затем импортировать функцию с тем же именем, исходная функция будет заменена и больше недоступна.

### <a name="finding-hidden-commands"></a>Поиск скрытых команд

Параметр **ALL** командлета [Get-Command](xref:Microsoft.PowerShell.Core.Get-Command) получает все команды с указанным именем, даже если они скрыты или заменены. Начиная с PowerShell 3,0, по умолчанию `Get-Command` получает только команды, которые выполняются при вводе имени команды.

В следующих примерах сеанс включает `Get-Date` функцию и командлет [Get-Date](xref:Microsoft.PowerShell.Utility.Get-Date) .

Следующая команда возвращает `Get-Date` команду, которая выполняется при вводе `Get-Date` .

```powershell
Get-Command Get-Date
```

```output
CommandType     Name                      ModuleName
-----------     ----                      ----------
Function        Get-Date
```

Следующая команда использует параметр **ALL** для получения всех `Get-Date` команд.

```powershell
Get-Command Get-Date -All
```

```output
CommandType     Name                      ModuleName
-----------     ----                      ----------
Function        Get-Date
Cmdlet          Get-Date                  Microsoft.PowerShell.Utility
```

### <a name="running-hidden-commands"></a>Выполнение скрытых команд

Вы можете выполнять определенные команды, указывая свойства элементов, которые отличают команду от других команд, которые могут иметь одно и то же имя. Этот метод можно использовать для выполнения любой команды, но он особенно полезен для выполнения скрытых команд.

#### <a name="qualified-names"></a>Полные имена

Использование имени командлета с указанием модуля позволяет выполнять команды, скрытые элементом с тем же именем. Например, можно выполнить `Get-Date` командлет, указав его имя модуля **Microsoft. PowerShell. Utility**.

Используйте этот предпочтительный метод при написании сценариев, которые планируется распространить. Нельзя предсказать, какие команды могут присутствовать в сеансе, в котором выполняется скрипт.

```powershell
New-Alias -Name "Get-Date" -Value "Get-ChildItem"
Microsoft.PowerShell.Utility\Get-Date
```

```output
Tuesday, September 4, 2018 8:17:25 AM
```

Чтобы выполнить `New-Map` команду, добавленную `MapFunctions` модулем, используйте полное имя модуля:

```powershell
MapFunctions\New-Map
```

Чтобы найти модуль, из которого была импортирована команда, используйте свойство **ModuleName** команд.

```
(Get-Command <command-name>).ModuleName
```

Например, чтобы найти источник `Get-Date` командлета, введите:

```powershell
(Get-Command Get-Date).ModuleName
```

```output
Microsoft.PowerShell.Utility
```

> [!NOTE]
> Нельзя указывать переменные или псевдонимы.

#### <a name="call-operator"></a>Оператор Call

Можно также использовать `Call` оператор `&` для выполнения скрытых команд, объединив его с вызовом [Get-ChildItem](xref:Microsoft.PowerShell.Management.Get-ChildItem) (псевдоним — "Dir") `Get-Command` или [Get-Module](xref:Microsoft.PowerShell.Core.Get-Module).

Оператор Call выполняет строки и блоки скриптов в дочерней области. Дополнительные сведения см. в разделе [about_Operators](about_Operators.md).

Например, если имеется функция с именем `Map` , которая скрыта псевдонимом с именем `Map` , используйте следующую команду для запуска функции.

```powershell
&(Get-Command -Name Map -CommandType Function)
```

or

```powershell
&(dir Function:\map)
```

Можно также сохранить скрытую команду в переменной, чтобы упростить ее выполнение.

Например, следующая команда сохраняет `Map` функцию в `$myMap` переменной, а затем использует `Call` оператор для его запуска.

```powershell
$myMap = (Get-Command -Name map -CommandType function)
&($myMap)
```

### <a name="replaced-items"></a>Замененные элементы

"Замененный" элемент — это тот, к которому вы больше не можете обращаться. Вы можете заменить элементы, импортировав элементы с тем же именем из модуля или оснастки.

Например, если вы вводите `Get-Map` функцию в сеансе и импортируете функцию с именем `Get-Map` , она заменяет исходную функцию. Его нельзя получить в текущем сеансе.

Переменные и псевдонимы не могут быть скрыты, так как для их выполнения нельзя использовать оператор Call или полное имя. При импорте переменных и псевдонимов из модуля или оснастки они заменяют переменные в сеансе с тем же именем.

### <a name="avoiding-name-conflicts"></a>Предотвращение конфликтов имен

Лучшим способом управления конфликтами имен команд является их предотвращение. При именовании команд используйте уникальное имя. Например, добавьте свои инициалы или аббревиатуру названия компании в существительные в командах.

Кроме того, при импорте команд в сеанс из модуля PowerShell или из другого сеанса используйте параметр командлета `Prefix` [Import-Module](xref:Microsoft.PowerShell.Core.Import-Module) или

Командлет [Import-PSSession](xref:Microsoft.PowerShell.Utility.Import-PSSession) для добавления префикса к существительным в именах команд.

Например, следующая команда позволяет избежать конфликтов с `Get-Date` `Set-Date` командлетами и, которые поставляются с PowerShell при импорте `DateFunctions` модуля.

```powershell
Import-Module -Name DateFunctions -Prefix ZZ
```

Дополнительные сведения см. в разделе `Import-Module` и `Import-PSSession` ниже.

## <a name="see-also"></a>См. также статью

- [about_Path_Syntax](about_Path_Syntax.md)
- [about_Aliases](about_Aliases.md)
- [about_Functions](about_Functions.md)
- [Alias-Provider](../../Microsoft.PowerShell.Core/About/about_Alias_Provider.md)
- [Function-Provider](../../Microsoft.PowerShell.Core/About/about_Function_Provider.md)
- [Get-Command](xref:Microsoft.PowerShell.Core.Get-Command)
- [Import-Module](xref:Microsoft.PowerShell.Core.Import-Module)
- [Import-PSSession](xref:Microsoft.PowerShell.Utility.Import-PSSession)