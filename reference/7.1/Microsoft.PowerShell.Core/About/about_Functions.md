---
description: Описание создания и использования функций в PowerShell.
keywords: powershell,командлет
Locale: en-US
ms.date: 2/27/2019
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-7.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Functions
ms.openlocfilehash: bef1f9f0b672f45c30626a1bbe4f2c6a7dfa540b
ms.sourcegitcommit: f874dc1d4236e06a3df195d179f59e0a7d9f8436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "93232709"
---
# <a name="about-functions"></a>О функциях

## <a name="short-description"></a>Краткое описание

Описание создания и использования функций в PowerShell.

## <a name="long-description"></a>Подробное описание

Функция — это список операторов PowerShell с назначенным именем. При запуске функции необходимо ввести имя функции. Инструкции в списке выполняются так, как если бы вы вводили их в командной строке.

Функции могут быть простыми:

```powershell
function Get-PowerShellProcess { Get-Process PowerShell }
```

Функция также может быть сложной в качестве командлета или программы приложения.

Как и командлеты, функции могут иметь параметры. Параметры могут быть именованными, позиционированными, переключателями или динамическими параметрами. Параметры функции можно считывать из командной строки или из конвейера.

Функции могут возвращать значения, которые могут быть отображены, назначены переменным или переданы другим функциям или командлетам. Также можно указать возвращаемое значение с помощью `return` ключевого слова. `return`Ключевое слово не влияет или не подавляет другие выходные данные, возвращаемые функцией. Однако `return` ключевое слово завершает функцию в этой строке. Дополнительные сведения см. в разделе [about_Return](about_Return.md).

Список операторов функции может содержать различные типы списков операторов с ключевыми словами `Begin` , `Process` и `End` . Эти списки инструкций обработают входные данные из конвейера по-разному.

Фильтр — это специальный тип функции, который использует `Filter` ключевое слово.

Функции также могут действовать как командлеты. Можно создать функцию, которая работает так же, как командлет, без использования `C#` программирования. Дополнительные сведения см. в разделе [about_Functions_Advanced](about_Functions_Advanced.md).

## <a name="syntax"></a>Синтаксис

Ниже приведен синтаксис функции.

```
function [<scope:>]<name> [([type]$parameter1[,[type]$parameter2])]
{
  param([type]$parameter1 [,[type]$parameter2])
  dynamicparam {<statement list>}
  begin {<statement list>}
  process {<statement list>}
  end {<statement list>}
}
```

Функция включает следующие элементы:

- `Function`Ключевое слово
- Область (необязательно)
- Выбранное имя
- Любое количество именованных параметров (необязательно)
- Одна или несколько команд PowerShell, заключенных в фигурные скобки `{}`

Дополнительные сведения о `Dynamicparam` ключевом слове и динамических параметрах в функциях см. в разделе [about_Functions_Advanced_Parameters](about_Functions_Advanced_Parameters.md).

## <a name="simple-functions"></a>Простые функции

Функции не обязательно должны быть очень сложными. Простейшие функции имеют следующий формат:

```
function <function-name> {statements}
```

Например, следующая функция запускает PowerShell с параметром Запуск от имени администратора.

```powershell
function Start-PSAdmin {Start-Process PowerShell -Verb RunAs}
```

Чтобы использовать функцию, введите: `Start-PSAdmin`

Чтобы добавить операторы в функцию, введите каждую инструкцию в отдельной строке или используйте точку с запятой `;` для разделения инструкций.

Например, следующая функция находит все `.jpg` файлы в каталогах текущего пользователя, которые были изменены после начальной даты.

```powershell
function Get-NewPix
{
  $start = Get-Date -Month 1 -Day 1 -Year 2010
  $allpix = Get-ChildItem -Path $env:UserProfile\*.jpg -Recurse
  $allpix | Where-Object {$_.LastWriteTime -gt $Start}
}
```

Вы можете создать панель элементов с полезными небольшими функциями. Добавьте эти функции в профиль PowerShell, как описано в [about_Profiles](about_Profiles.md) и далее в этом разделе.

## <a name="function-names"></a>Имена функций

Функции можно назначить любое имя, но функции, к которым вы предоставили доступ другим, должны соответствовать правилам именования, установленным для всех команд PowerShell.

Имена функций должны состоять из пары существительных глаголов, в которых команда определяет действие, выполняемое функцией, а существительное определяет элемент, на котором командлет выполняет свое действие.

Функции должны использовать стандартные команды, которые были утверждены для всех команд PowerShell. Эти команды помогают нам упростить, согласовать и легко понимать имена команд.

Дополнительные сведения о стандартных командах PowerShell см. в разделе [утвержденные команды](/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands) в документация Майкрософт.

## <a name="functions-with-parameters"></a>Функции с параметрами

Параметры можно использовать с функциями, в том числе с именованными параметрами, параметрами, параметрами и динамическими параметрами. Дополнительные сведения о динамических параметрах в функциях см. в разделе [about_Functions_Advanced_Parameters](about_Functions_Advanced_Parameters.md).

### <a name="named-parameters"></a>именованных параметров

Можно определить любое количество именованных параметров. Можно включить значение по умолчанию для именованных параметров, как описано далее в этом разделе.

Параметры внутри фигурных скобок можно определить с помощью `Param` ключевого слова, как показано в следующем примере синтаксиса:

```
function <name> {
  param ([type]$parameter1[,[type]$parameter2])
  <statement list>
}
```

Можно также определить параметры за пределами фигурных скобок без `Param` ключевого слова, как показано в следующем примере синтаксиса:

```powershell
function <name> [([type]$parameter1[,[type]$parameter2])] {
  <statement list>
}
```

Ниже приведен пример альтернативного синтаксиса.

```powershell
Function Add-Numbers($one, $two) {
    $one + $two
}
```

Хотя первый метод является предпочтительным, разница между этими двумя методами отсутствует.

При запуске функции значение, указываемое для параметра, присваивается переменной, содержащей имя параметра. Значение этой переменной может использоваться в функции.

В следующем примере показана функция с именем `Get-SmallFiles` . Эта функция имеет `$Size` параметр. Функция отображает все файлы, размер которых меньше значения `$Size` параметра, и исключает каталоги.

```powershell
function Get-SmallFiles {
  Param($Size)
  Get-ChildItem $HOME | Where-Object {
    $_.Length -lt $Size -and !$_.PSIsContainer
  }
}
```

В функции можно использовать `$Size` переменную, которая является именем, определенным для параметра.

Чтобы использовать эту функцию, введите следующую команду:

```powershell
Get-SmallFiles -Size 50
```

Можно также ввести значение для именованного параметра без имени параметра.
Например, следующая команда дает тот же результат, что и команда, которая присваивает имя параметру **size** :

```powershell
Get-SmallFiles 50
```

Чтобы определить значение по умолчанию для параметра, введите знак равенства и значение после имени параметра, как показано в следующем варианте `Get-SmallFiles` примера:

```powershell
function Get-SmallFiles ($Size = 100) {
  Get-ChildItem $HOME | Where-Object {
    $_.Length -lt $Size -and !$_.PSIsContainer
  }
}
```

Если ввести `Get-SmallFiles` без значения, функция присваивает 100 значение `$size` . Если указать значение, то функция использует это значение.

При необходимости можно указать краткую строку справки, описывающую значение параметра по умолчанию, добавив атрибут **псдефаултвалуе** в описание параметра и указав свойство **Help** объекта **псдефаултвалуе**. Чтобы предоставить строку справки, описывающую значение по умолчанию (100) параметра **size** в `Get-SmallFiles` функции, добавьте атрибут **псдефаултвалуе** , как показано в следующем примере.

```powershell
function Get-SmallFiles {
  param (
      [PSDefaultValue(Help = '100')]
      $Size = 100
  )
}
```

Дополнительные сведения о классе атрибута **псдефаултвалуе** см. в разделе [псдефаултвалуе Attribute Members](/dotnet/api/system.management.automation.psdefaultvalueattribute).

### <a name="positional-parameters"></a>Параметры позиционирования

Параметр с заданной позицией — это параметр без имени параметра. PowerShell использует порядок значений параметра, чтобы связать каждое значение параметра с параметром в функции.

При использовании позиционированных параметров введите одно или несколько значений после имени функции. Значения позиционированных параметров присваиваются `$args` переменной массива.
Значение, следующее за именем функции, присваивается первой положению в `$args` массиве, `$args[0]` .

Следующая `Get-Extension` функция добавляет `.txt` расширение имени файла к указанному имени файла:

```powershell
function Get-Extension {
  $name = $args[0] + ".txt"
  $name
}
```

```powershell
Get-Extension myTextFile
```

```Output
myTextFile.txt
```

### <a name="switch-parameters"></a>Параметры переключателя

Переключатель — это параметр, который не требует значения. Вместо этого введите имя функции, за которым следует имя параметра переключателя.

Чтобы определить параметр переключателя, укажите тип `[switch]` перед именем параметра, как показано в следующем примере:

```powershell
function Switch-Item {
  param ([switch]$on)
  if ($on) { "Switch on" }
  else { "Switch off" }
}
```

При вводе `On` параметра Switch после имени функции функция отображает параметр on. Без параметра Switch отображается значение "Отключить выключение".

```powershell
Switch-Item -on
```

```Output
Switch on
```

```powershell
Switch-Item
```

```Output
Switch off
```

При выполнении функции можно также присвоить **логическое** значение параметру, как показано в следующем примере:

```powershell
Switch-Item -on:$true
```

```Output
Switch on
```

```powershell
Switch-Item -on:$false
```

```Output
Switch off
```

## <a name="using-splatting-to-represent-command-parameters"></a>Использование Сплаттинг для представления параметров команды

Сплаттинг можно использовать для представления параметров команды. Эта функция появилась в Windows PowerShell 3,0.

Используйте этот метод в функциях, вызывающих команды в сеансе. Вам не нужно объявлять или перечислять параметры команды или изменять функцию при изменении параметров команды.

Следующий пример функции вызывает `Get-Command` командлет. Команда использует `@Args` для представления параметров `Get-Command` .

```powershell
function Get-MyCommand { Get-Command @Args }
```

`Get-Command`При вызове функции можно использовать все параметры `Get-MyCommand` . Параметры и значения параметров передаются в команду с помощью команды `@Args` .

```powershell
Get-MyCommand -Name Get-ChildItem
```

```Output
CommandType     Name                ModuleName
-----------     ----                ----------
Cmdlet          Get-ChildItem       Microsoft.PowerShell.Management
```

Эта `@Args` функция использует `$Args` Автоматический параметр, представляющий необъявленные параметры и значения командлета из оставшихся аргументов.

Дополнительные сведения о Сплаттинг см. в разделе [about_Splatting](about_Splatting.md).

## <a name="piping-objects-to-functions"></a>Передача объектов в функции

Любая функция может принимать входные данные из конвейера. Можно контролировать, как функция обрабатывает входные данные из конвейера с помощью `Begin` `Process` `End` ключевых слов, и. В следующем образце синтаксиса показаны три ключевых слова:

```
function <name> {
  begin {<statement list>}
  process {<statement list>}
  end {<statement list>}
}
```

`Begin`Список инструкций выполняется только один раз в начале функции.

> [!IMPORTANT]
> Если функция определяет `Begin` блок, то `Process` `End` весь код должен находиться внутри этих блоков. Код не будет располагаться за пределами блоков, если определены *какие либо* блоки.

`Process`Список инструкций выполняется один раз для каждого объекта в конвейере.
Во время `Process` выполнения блока каждый объект конвейера назначается `$_` автоматической переменной, по одному объекту конвейера за раз.

После того как функция получит все объекты в конвейере, `End` список инструкций будет выполняться один раз. Если не `Begin` `Process` `End` используются ключевые слова, или, все инструкции рассматриваются как `End` список инструкций.

Следующая функция использует `Process` ключевое слово. Функция отображает примеры из конвейера:

```powershell
function Get-Pipeline
{
  process {"The value is: $_"}
}
```

Чтобы продемонстрировать эту функцию, введите список чисел, разделенных запятыми, как показано в следующем примере:

```powershell
1,2,4 | Get-Pipeline
```

```Output
The value is: 1
The value is: 2
The value is: 4
```

При использовании функции в конвейере объекты, переданный функции, назначаются `$input` автоматической переменной. Функция выполняет инструкции с `Begin` ключевым словом перед тем, как все объекты поступают из конвейера. Функция выполняет инструкции с `End` ключевым словом после того, как все объекты были получены из конвейера.

В следующем примере показана `$input` Автоматическая переменная с `Begin` `End` ключевыми словами и.

```powershell
function Get-PipelineBeginEnd
{
  begin {"Begin: The input is $input"}
  end {"End:   The input is $input" }
}
```

Если эта функция выполняется с помощью конвейера, отображаются следующие результаты.

```powershell
1,2,4 | Get-PipelineBeginEnd
```

```Output
Begin: The input is
End:   The input is 1 2 4
```

При `Begin` выполнении инструкции функция не имеет входных данных из конвейера. `End`Инструкция выполняется после того, как функция применяет значения.

Если у функции есть `Process` ключевое слово, каждый объект в удаляется `$input` из `$input` и присваивается `$_` . В следующем примере содержится `Process` список операторов:

```powershell
function Get-PipelineInput
{
  process {"Processing:  $_ " }
  end {"End:   The input is: $input" }
}
```

В этом примере каждый объект, передаваемый функции, отправляется в `Process` список инструкций. `Process`Инструкции выполняются для каждого объекта, по одному объекту за раз. `$input`Автоматическая переменная пуста, если функция достигает `End` ключевого слова.

```powershell
1,2,4 | Get-PipelineInput
```

```Output
Processing:  1
Processing:  2
Processing:  4
End:   The input is:
```

Дополнительные сведения см. [в разделе Использование перечислителей](about_Automatic_Variables.md#using-enumerators) .

## <a name="filters"></a>Фильтры

Фильтр — это тип функции, которая выполняется для каждого объекта в конвейере. Фильтр напоминает функцию со всеми ее операторами в `Process` блоке.

Синтаксис фильтра выглядит следующим образом:

```
filter [<scope:>]<name> {<statement list>}
```

Следующий фильтр принимает записи журнала из конвейера, а затем отображает всю запись или только часть сообщения в записи:

```powershell
filter Get-ErrorLog ([switch]$message)
{
  if ($message) { Out-Host -InputObject $_.Message }
  else { $_ }
}
```

## <a name="function-scope"></a>Область действия функции

Функция существует в области, в которой она была создана.

Если функция является частью скрипта, функция доступна для инструкций внутри этого скрипта. По умолчанию функция в скрипте недоступна в командной строке.

Можно указать область функции. Например, функция добавляется в глобальную область в следующем примере:

```powershell
function global:Get-DependentSvs {
  Get-Service | Where-Object {$_.DependentServices}
}
```

Если функция находится в глобальной области, ее можно использовать в скриптах, функциях и в командной строке.

Обычно функции создают область. Элементы, созданные в функции, такие как переменные, существуют только в области видимости функции.

Дополнительные сведения об области действия в PowerShell см. в разделе [about_Scopes](about_Scopes.md).

## <a name="finding-and-managing-functions-using-the-function-drive"></a>Поиск функций и управление ими с помощью диска Function:

Все функции и фильтры в PowerShell автоматически сохраняются на `Function:` диске. Этот диск предоставляется поставщиком **функций** PowerShell.

При обращении к `Function:` диску введите двоеточие после **функции** , как при обращении к `C` диску или на `D` диске компьютера.

Следующая команда отображает все функции в текущем сеансе PowerShell:

```powershell
Get-ChildItem function:
```

Команды в функции хранятся в виде блока скрипта в свойстве определения функции. Например, чтобы отобразить команды в функции справки, поставляемой с PowerShell, введите:

```powershell
(Get-ChildItem function:help).Definition
```

Можно также использовать следующий синтаксис.

```powershell
$function:help
```

Дополнительные сведения о `Function:` диске см. в разделе справки по поставщику **функций** . Введите `Get-Help Function`.

## <a name="reusing-functions-in-new-sessions"></a>Повторное использование функций в новых сеансах

При вводе функции в командной строке PowerShell функция станет частью текущего сеанса. Он доступен до завершения сеанса.

Чтобы использовать функцию во всех сеансах PowerShell, добавьте функцию в профиль PowerShell. Дополнительные сведения о профилях см. в разделе [about_Profiles](about_Profiles.md).

Можно также сохранить функцию в файле сценария PowerShell. Введите функцию в текстовом файле, а затем сохраните файл с `.ps1` расширением имени файла.

## <a name="writing-help-for-functions"></a>Написание справки для функций

`Get-Help`Командлет возвращает справку по функциям, а также к командлетам, поставщикам и скриптам. Чтобы получить справку по функции, введите, `Get-Help` за которым следует имя функции.

Например, чтобы получить справку по `Get-MyDisks` функции, введите:

```powershell
Get-Help Get-MyDisks
```

Вы можете написать справку для функции с помощью любого из двух следующих методов:

- Comment-Based справки по функциям

  Создайте раздел справки, используя специальные ключевые слова в комментариях. Чтобы создать справку на основе комментариев для функции, комментарии должны располагаться в начале или в конце тела функции или в строках, предшествующих ключевому слову Function. Дополнительные сведения о справке на основе комментариев см. в разделе [about_Comment_Based_Help](about_Comment_Based_Help.md).

- XML-Based справки по функциям

  Создайте раздел справки на основе XML, например тип, который обычно создается для командлетов. При локализации разделов справки на несколько языков требуется справка на основе XML.

  Чтобы связать функцию с разделом справки на основе XML, используйте `.ExternalHelp` ключевое слово справки на основе комментариев. Без этого ключевого слова `Get-Help` не удается найти раздел справки по функциям и вызовы для `Get-Help` функции, возвращающие только автоматически созданную справку.

  Дополнительные сведения о `ExternalHelp` ключевом слове см. в разделе [about_Comment_Based_Help](about_Comment_Based_Help.md). Дополнительные сведения о справке на основе XML см. в разделе [как написать справку по командлетам](https://go.microsoft.com/fwlink/?LinkID=123415) в библиотеке MSDN.

## <a name="see-also"></a>См. также статью

[about_Automatic_Variables](about_Automatic_Variables.md)

[about_Comment_Based_Help](about_Comment_Based_Help.md)

[about_Functions_Advanced](about_Functions_Advanced.md)

[about_Functions_Advanced_Methods](about_Functions_Advanced_Methods.md)

[about_Functions_Advanced_Parameters](about_Functions_Advanced_Parameters.md)

[about_Functions_CmdletBindingAttribute](about_Functions_CmdletBindingAttribute.md)

[about_Functions_OutputTypeAttribute](about_Functions_OutputTypeAttribute.md)

[about_Parameters](about_Parameters.md)

[about_Profiles](about_Profiles.md)

[about_Scopes](about_Scopes.md)

[about_Script_Blocks](about_Script_Blocks.md)

[about_Function_provider](about_Function_provider.md)
