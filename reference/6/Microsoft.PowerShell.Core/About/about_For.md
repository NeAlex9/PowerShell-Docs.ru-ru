---
description: Описывает команду языка, которую можно использовать для выполнения инструкций на основе условного теста.
keywords: powershell,командлет
Locale: en-US
ms.date: 3/4/2019
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_for?view=powershell-6&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_For
ms.openlocfilehash: 5f4fc025ee36e99de7d2ad7a00b1c1dca9c5ce3f
ms.sourcegitcommit: f874dc1d4236e06a3df195d179f59e0a7d9f8436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "93231482"
---
# <a name="about-for"></a>О программе для

## <a name="short-description"></a>Краткое описание
Описывает команду языка, которую можно использовать для выполнения инструкций на основе условного теста.

## <a name="long-description"></a>Подробное описание

`For`Оператор (также называемый `For` циклом) — это языковая конструкция, которую можно использовать для создания цикла, запускающего команды в блоке команд, пока заданное условие принимает значение `$true` .

Обычно `For` цикл используется для прохода по массиву значений и для работы с подмножеством этих значений. В большинстве случаев, если необходимо выполнить итерацию всех значений в массиве, рассмотрите возможность использования `Foreach` оператора.

### <a name="syntax"></a>Синтаксис

Ниже показан `For` синтаксис инструкции.

```
for (<Init>; <Condition>; <Repeat>)
{
    <Statement list>
}
```

Заполнитель **init** представляет одну или несколько команд, выполняемых перед началом цикла. Для создания и инициализации переменной с начальным значением обычно используется часть **init** инструкции.

Эта переменная будет использоваться в качестве основания для проверки условия в следующей части `For` инструкции.

Заполнитель **условия** представляет часть `For` инструкции, которая разрешается в `$true` `$false` **логическое** значение или. PowerShell оценивает условие при каждом `For` выполнении цикла. Если инструкция имеет значение `$true` , команды в блоке команд выполняются, а инструкция вычисляется снова. Если условие по-прежнему выполняется `$true` , команды в **списке инструкций** выполняются снова. Цикл повторяется до тех пор, пока не будет выполнено условие `$false` .

Заполнитель **Repeat** представляет одну или несколько команд, разделенных запятыми, которые выполняются каждый раз при повторении цикла. Как правило, он используется для изменения переменной, которая проверяется внутри **условия** инструкции.

Заполнитель **списка инструкций** представляет набор из одной или нескольких команд, которые выполняются при каждом входе или повторении цикла. Содержимое **списка инструкций** заключено в фигурные скобки.

### <a name="support-for-multiple-operations"></a>Поддержка нескольких операций

Для нескольких операций присваивания в операторе **init** поддерживаются следующие синтаксисы:

```powershell
# Comma separated assignment expressions enclosed in parenthesis.
for (($i = 0), ($j = 0); $i -lt 10; $i++)
{
    "`$i:$i"
    "`$j:$j"
}

# Sub-expression using the semicolon to separate statements.
for ($($i = 0;$j = 0); $i -lt 10; $i++)
{
    "`$i:$i"
    "`$j:$j"
}
```

Для нескольких операций присваивания в операторе **Repeat** поддерживаются следующие синтаксисы:

```powershell
# Comma separated assignment expressions.
for (($i = 0), ($j = 0); $i -lt 10; $i++)
{
    "`$i:$i"
    "`$j:$j"
}

# Comma separated assignment expressions enclosed in parenthesis.
for (($i = 0), ($j = 0); $i -lt 10; ($i++), ($j++))
{
    "`$i:$i"
    "`$j:$j"
}

# Sub-expression using the semicolon to separate statements.
for ($($i = 0;$j = 0); $i -lt 10; $($i++;$j++))
{
    "`$i:$i"
    "`$j:$j"
}
```

> [!NOTE]
> Операции, отличные от pre или Increment, могут не работать со всеми синтаксисами.

Для нескольких **условий** используйте логические операторы, как показано в следующем примере.

```powershell
for (($i = 0), ($j = 0); $i -lt 10 -and $j -lt 10; $i++,$j++)
{
    "`$i:$i"
    "`$j:$j"
}
```

Дополнительные сведения см. в разделе [about_Logical_Operators](about_Logical_Operators.md).

### <a name="examples"></a>Примеры

Как минимум, `For` оператор требует круглых скобок, окружающих **init** , **Condition** и **Repeat** , а также команду, заключенную в фигурные скобки в части оператора **List** .

Обратите внимание, что будущие примеры намеренно демонстрируют код за пределами `For` оператора. В последующих примерах код интегрируется в `For` инструкцию.

Например, следующая `For` инструкция непрерывно отображает значение `$i` переменной, пока вы не выйдете из команды вручную, нажав клавиши CTRL + C.

```powershell
$i = 1
for (;;)
{
    Write-Host $i
}
```

В список инструкций можно добавить дополнительные команды, чтобы значение `$i` увеличивалось на 1 каждый раз при выполнении цикла, как показано в следующем примере.

```powershell
for (;;)
{
    $i++; Write-Host $i
}
```

До выхода из команды нажатием клавиш CTRL + C эта инструкция будет постоянно отображать значение `$i` переменной, так как оно увеличивается на 1 при каждом выполнении цикла.

Вместо того, чтобы изменять значение переменной в списке инструкций `For` , можно использовать **повторную** часть `For` инструкции, как показано ниже.

```powershell
$i=1
for (;;$i++)
{
    Write-Host $i
}
```

Эта инструкция по-прежнему будет повторяться бессрочно, пока вы не завершите выполнение команды, нажав клавиши CTRL + C.

Можно завершить цикл, `For` используя *условие* . Условие можно разместить с помощью части **Condition** `For` инструкции. `For`Цикл завершается, когда условие принимает значение `$false` .

В следующем примере `For` цикл выполняется, пока значение `$i` меньше или равно 10.

```powershell
$i=1
for(;$i -le 10;$i++)
{
    Write-Host $i
}
```

Вместо создания и инициализации переменной за пределами `For` инструкции эту задачу можно выполнить внутри `For` цикла, используя часть **init** `For` инструкции.

```powershell
for($i=1; $i -le 10; $i++){Write-Host $i}
```

Вместо точек с запятой можно использовать символы возврата каретки, чтобы ограничить количество частей инструкции **init** , **Condition** и **Repeat** `For` . В следующем примере показан объект `For` , который использует этот альтернативный синтаксис.

```powershell
for ($i = 0
  $i -lt 10
  $i++){
  $i
}
```

Эта альтернативная форма `For` инструкции работает в файлах скриптов PowerShell и в командной строке PowerShell. Однако `For` при вводе интерактивных команд в командной строке проще использовать синтаксис инструкции с точкой с запятой.

`For`Цикл является более гибким, чем `Foreach` цикл, поскольку он позволяет увеличивать значения в массиве или коллекции с помощью шаблонов. В следующем примере `$i` переменная увеличивается на 2 в **повторяющейся** части `For` инструкции.

```powershell
for ($i = 0; $i -le 20; $i += 2)
{
    Write-Host $i
}
```

`For`Цикл также можно записать на одной строке, как показано в следующем примере.

```powershell
for ($i = 0; $i -lt 10; $i++) { Write-Host $i }
```

## <a name="see-also"></a>СМ. ТАКЖЕ

[about_Comparison_Operators](about_Comparison_Operators.md)

[about_Foreach](about_Foreach.md)