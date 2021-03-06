---
description: Описывает схемы синтаксиса, используемые в PowerShell.
ms.date: 06/27/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_command_syntax?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Command_Syntax
ms.openlocfilehash: 8182cc856de0813f0828400bcef7170a6e165c51
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "99600677"
---
# <a name="about-command-syntax"></a>О синтаксисе команд

## <a name="short-description"></a>КРАТКОЕ ОПИСАНИЕ
Описывает схемы синтаксиса, используемые в PowerShell.

## <a name="long-description"></a>ПОДРОБНОЕ ОПИСАНИЕ

Командлеты [Get-Help](xref:Microsoft.PowerShell.Core.Get-Help) и [Get-Command](xref:Microsoft.PowerShell.Core.Get-Command) отображают схемы синтаксиса, помогающие правильно создавать команды. В этом разделе объясняется, как интерпретировать схемы синтаксиса.

## <a name="syntax-diagrams"></a>СХЕМЫ СИНТАКСИСА

Каждый абзац на схеме синтаксиса команд представляет допустимую форму команды.

Чтобы создать команду, следуйте схеме синтаксиса слева направо. Выберите из необязательных параметров и укажите значения для заполнителей.

PowerShell использует следующую нотацию для схем синтаксиса.

```powershell
<command-name> -<Required Parameter Name> <Required Parameter Value>
[-<Optional Parameter Name> <Optional Parameter Value>]
[-<Optional Switch Parameters>]
[-<Optional Parameter Name>] <Required Parameter Value>
```

Ниже приведен синтаксис командлета [New-Alias](xref:Microsoft.PowerShell.Utility.New-Alias) .

```powershell
New-Alias [-Name] <string> [-Value] <string> [-Description <string>]
[-Force] [-Option {None | ReadOnly | Constant | Private | AllScope}]
[-PassThru] [-Scope <string>] [-Confirm] [-WhatIf] [<CommonParameters>]
```

Синтаксис задается прописными буквами для удобства чтения, но в PowerShell регистр не учитывается.

Схема синтаксиса содержит следующие элементы.

## <a name="command-name"></a>Имя команды

Команды всегда начинаются с имени команды, например `New-Alias` . Введите имя команды или ее псевдоним, например "gcm" для `Get-Command` .

## <a name="parameters"></a>Параметры

Параметры команды — это параметры, определяющие действие команды.
Некоторые параметры принимают значение "value", которое является входным пользователем для команды.

Например, `Get-Help` команда имеет параметр **Name** , который позволяет указать имя раздела, для которого отображается справка. Имя раздела — это значение параметра **Name** .

В команде PowerShell имена параметров всегда начинаются с дефиса.
Дефис сообщает PowerShell, что элемент в команде является именем параметра.

Например, чтобы использовать параметр Name параметра `New-Alias` , введите следующее:

```powershell
-Name
```

Параметры могут быть обязательными или необязательными. В схеме синтаксиса необязательные элементы заключаются в квадратные скобки `[ ]` .

Дополнительные сведения о параметрах см. в разделе [about_Parameters](about_Parameters.md).

## <a name="parameter-values"></a>Значения параметров

Значение параметра — это входные данные, которые принимает параметр. Поскольку оболочка Windows PowerShell основана на Microsoft .NET Framework, значения параметров представлены на схеме синтаксиса по типу .NET.

Например, параметр name `Get-Help` принимает значение «String», представляющее собой текстовую строку, например одно слово или несколько слов, заключенных в кавычки.

```powershell
[-Name] <string>
```

Тип .NET значения параметра заключен в угловые скобки `< >` , чтобы указать, что он является заполнителем для значения, а не литералом, введенным в команде.

Чтобы использовать параметр, замените заполнитель типа .NET объектом с указанным типом .NET.

Например, чтобы использовать параметр **Name** , введите "-Name", а затем строку, как показано ниже.

```powershell
-Name MyAlias
```

## <a name="parameters-with-no-values"></a>Параметры без значений

Некоторые параметры не принимают входные данные, поэтому они не имеют значения параметра.
Параметры без значений называются параметрами-переключателями, так как они работают как параметры on/off. Вы включаете их (on) или не пропускаете их (OFF) из команды.

Чтобы использовать параметр Switch, просто введите имя параметра, перед которым следует дефис.

Например, чтобы использовать параметр **WhatIf** `New-Alias` командлета, введите следующее:

```powershell
-WhatIf
```

## <a name="parameter-sets"></a>Наборы параметров

Параметры команды перечислены в наборах параметров. Наборы параметров выглядят как абзацы схемы синтаксиса.

`New-Alias`Командлет имеет один набор параметров, но многие командлеты имеют несколько наборов параметров. Некоторые параметры командлета уникальны для набора параметров, а другие — в нескольких наборах параметров. Каждый набор параметров представляет формат допустимой команды. Набор параметров включает в себя только параметры, которые можно использовать вместе в команде. Если параметры не могут использоваться в одной команде, они отображаются в отдельных наборах параметров.

Например, командлет [Get-Random](xref:Microsoft.PowerShell.Utility.Get-Random) имеет следующие наборы параметров:

```powershell
Get-Random [[-Maximum] <Object>] [-Minimum <Object>] [-SetSeed <int>]
[<CommonParameters>]

Get-Random [-InputObject] <Object[]> [-Count <int>] [-SetSeed <int>]
[<CommonParameters>]
```

Первый набор параметров, который возвращает случайное число, имеет **минимальные** и **максимальные** параметры. Второй набор параметров, который возвращает случайно выбранный объект из набора объектов, включает параметры **InputObject** и **Count** . Оба набора параметров имеют параметр **SetSeed** и общие параметры.

Эти наборы параметров указывают, что можно использовать параметры **InputObject** и **Count** в одной команде, но нельзя использовать параметры **Maximum** и **Count** в одной и той же команде.

Вы указываете, какой набор параметров следует использовать, с помощью параметров в этом наборе параметров.

Однако у каждого командлета также есть набор параметров по умолчанию. Набор параметров по умолчанию используется, если не указаны параметры, уникальные для набора параметров. Например, если вы используете `Get-Random` без параметров, Windows PowerShell предполагает, что вы используете набор **числовых** параметров и возвращает случайное число.

В каждом наборе параметров параметры отображаются в порядке расположения. Порядок параметров в команде имеет значение только в том случае, если не заданы имена необязательных параметров. Если имена параметров опущены, PowerShell присваивает значения параметрам по положению и типу. Дополнительные сведения о положении параметра см. в разделе `about_Parameters` .

## <a name="symbols-in-syntax-diagrams"></a>Символы в схемах синтаксиса

На схеме синтаксиса перечислены имя команды, параметры команды и значения параметров. В нем также используются символы, чтобы продемонстрировать, как создать допустимую команду.

Схемы синтаксиса используют следующие символы:

- Дефис `-` обозначает имя параметра. В команде введите дефис непосредственно перед именем параметра без промежуточных пробелов, как показано на схеме синтаксиса.

  Например, чтобы использовать параметр **Name** типа `New-Alias` , введите:

  ```powershell
  -Name
  ```

- Угловые скобки `<>` обозначают текст заполнителя. В команде не вводите угловые скобки или текст заполнителя. Вместо этого замените его элементом, который он описывает.

  Угловые скобки используются для задания типа .NET значения, принимаемого параметром. Например, чтобы использовать параметр **Name** `New-Alias` командлета, замените на `<string>` строку, представляющую собой одно слово или группу слов, заключенных в кавычки.

- Квадратные скобки `[ ]` обозначают необязательные элементы. Параметр и его значение могут быть необязательными, или имя обязательного параметра может быть необязательным.

  Например, параметр **Description** аргумента `New-Alias` и его значение заключаются в квадратные скобки, так как они являются необязательными.

  ```powershell
  [-Description <string>]
  ```

  Квадратные скобки также указывают, что значение параметра name `<string>` является обязательным, но имя параметра "имя" является необязательным.

  ```powershell
  [-Name] <string>
  ```

- Правая и левая скобки, `[]` добавленные к типу .NET, указывают на то, что параметр может принимать одно или несколько значений этого типа. Введите значения в список с разделителями-запятыми.

  Например, параметр **Name** `New-Alias` командлета принимает только одну строку, но параметр **Name** для [Get-Process](xref:Microsoft.PowerShell.Management.Get-Process) может принимать одну или несколько строк.

  ```powershell
  New-Alias [-Name] <string>

  New-Alias -Name MyAlias
  ```

  ```powershell
  Get-Process [-Name] <string[]>

  Get-Process -Name Explorer, Winlogon, Services
  ```

- Фигурные скобки `{}` обозначают "перечисление", которое представляет собой набор допустимых значений для параметра.

  Значения в фигурных скобках разделяются вертикальными линиями `|` . Эти строки указывают на «эксклюзивный» выбор, что означает, что можно выбрать только одно значение из набора значений, перечисленных внутри фигурных скобок.

  Например, синтаксис для `New-Alias` командлета включает следующее перечисление значений для параметра **Option** :

  ```powershell
  -Option {None | ReadOnly | Constant | Private | AllScope}
  ```

  Фигурные скобки и вертикальные линии указывают, что можно выбрать одно из перечисленных значений **для параметра параметра** , например "ReadOnly" или "AllScope".

  ```powershell
  -Option ReadOnly
  ```

## <a name="optional-items"></a>Необязательные элементы

Необязательные элементы заключены в квадратные скобки `[]` . Например, в `New-Alias` описании синтаксиса командлета параметр **Scope** является необязательным. Это указывается в синтаксисе квадратными скобками вокруг имени параметра и типа:

```powershell
[-Scope <string>]
```

Ниже приведены правильные примеры использования `New-Alias` командлета.

```powershell
New-Alias -Name utd -Value Update-TypeData
New-Alias -Name utd -Value Update-TypeData -Scope Global
```

Имя параметра может быть необязательным, даже если значение для этого параметра является обязательным. Это указывается в синтаксисе квадратными скобками вокруг имени параметра, но не типа параметра, как в этом примере из `New-Alias` командлета:

```powershell
[-Name] <string> [-Value] <string>
```

Следующие команды правильно используют `New-Alias` командлет. Эти команды дают тот же результат.

```powershell
New-Alias -Name utd -Value Update-TypeData
New-Alias -Name utd Update-TypeData
New-Alias utd -Value Update-TypeData
New-Alias utd Update-TypeData
```

Если имя параметра не включено в инструкцию как типизированное, Windows PowerShell пытается использовать расположение аргументов для присвоения значений параметрам.

Следующий пример не завершен:

```powershell
New-Alias utd
```

Для этого командлета требуются значения как для параметров **имени** , так и для **значения** .

В примерах синтаксиса скобки также используются при именовании и приведении к типам платформа .NET Framework. В этом контексте квадратные скобки не указывают, что элемент является необязательным.

## <a name="see-also"></a>СМ. ТАКЖЕ

- [about_Parameters](about_Parameters.md)
- [Get-Command](xref:Microsoft.PowerShell.Core.Get-Command)
- [Get-Help](xref:Microsoft.PowerShell.Core.Get-Help)

