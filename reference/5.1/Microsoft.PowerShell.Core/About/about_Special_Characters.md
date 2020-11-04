---
description: Описание специальных последовательностей символов, управляющих тем, как PowerShell интерпретирует следующие символы в последовательности.
keywords: powershell,командлет
Locale: en-US
ms.date: 04/04/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_special_characters?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Special_Characters
ms.openlocfilehash: 875a1c3c63e759151c3c64b5396312b030955cb7
ms.sourcegitcommit: f874dc1d4236e06a3df195d179f59e0a7d9f8436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "93231925"
---
# <a name="about-special-characters"></a>О специальных символах

## <a name="short-description"></a>Краткое описание

Описание специальных последовательностей символов, управляющих тем, как PowerShell интерпретирует следующие символы в последовательности.

## <a name="long-description"></a>Подробное описание

PowerShell поддерживает набор специальных последовательностей символов, которые используются для представления символов, не входящих в стандартную кодировку. Последовательности обычно называют _escape-последовательностями_ .

Escape-последовательности начинаются с символа обратной косой черты, называемого грависом (ASCII 96), и учитывают регистр. Символ обратной кавычки также может называться Escape- _символом_ .

Escape-последовательности обрабатываются только в строках, содержащихся в двойных кавычках ( `"` ).

PowerShell распознает следующие escape-последовательности:

|  Последовательность   |       Описание       |
| ----------- | ----------------------- |
| `` `0 ``    | NULL                    |
| `` `a ``    | Оповещение                   |
| `` `b ``    | Отмена               |
| `` `f ``    | Перевод страницы               |
| `` `n ``    | Новая строка                |
| `` `r ``    | Возврат каретки         |
| `` `t ``    | Горизонтальная табуляция          |
| `` `v ``    | Вертикальная табуляция            |

Кроме того, PowerShell имеет специальный маркер, помечающий, где следует останавливаться при разборе. Все символы, которые следуют за этим маркером, используются в качестве литеральных значений, которые не интерпретируемы.

Специальный маркер синтаксического анализа:

| Последовательность |            Описание             |
| -------- | ---------------------------------- |
| `--%`    | Завершите синтаксический анализ всех следующих элементов |

## <a name="null-0"></a>NULL (' 0)

Символ null ( `` `0 `` ) отображается как пустое пространство в выходных данных PowerShell.
Эта функция позволяет использовать PowerShell для чтения и обработки текстовых файлов, использующих нуль символов, таких как завершение строк или индикаторы завершения записи. Специальный символ NULL не эквивалентен `$null` переменной, в которой хранится значение **null** .

## <a name="alert-a"></a>Предупреждение (' а)

Символ предупреждения ( `` `a `` ) отправляет звуковой сигнал на динамик компьютера.
Этот символ можно использовать для предупреждения пользователя о предопределенном действии. В следующем примере два звуковых сигнала отправляются на динамик локального компьютера.

```powershell
for ($i = 0; $i -le 1; $i++){"`a"}
```

## <a name="backspace-b"></a>Backspace (' б)

Символ Backspace ( `` `b `` ) перемещает курсор назад на один символ, но не удаляет символы.

Этот пример записывает слово **BACKUP** , а затем дважды перемещает курсор назад.
Затем в новой позиции записывается пробел, за которым следует слово **out** .

```powershell
"backup`b`b out"
```

```Output
back out
```

## <a name="form-feed-f"></a>Веб-канал формы (' ' f ' ')

Символ перевода формы ( `` `f `` ) представляет собой инструкцию PRINT, которая извлекает текущую страницу и продолжит печать на следующей странице. Символ перевода формы влияет только на печатные документы. Он не влияет на вывод на экран.

## <a name="new-line-n"></a>Новая строка (' n)

Символ новой строки ( `` `n `` ) вставляет разрыв строки сразу после символа.

В этом примере показано, как использовать символ новой строки для создания разрывов строк в `Write-Host` команде.

```powershell
"There are two line breaks to create a blank line`n`nbetween the words."
```

```Output
There are two line breaks to create a blank line

between the words.
```

## <a name="carriage-return-r"></a>Возврат каретки (' r)

Символ возврата каретки ( `` `r `` ) перемещает выходной курсор в начало текущей строки и продолжается запись. Все символы в текущей строке перезаписываются.

В этом примере текст перед возвратом каретки перезаписывается.

```powershell
Write-Host "These characters are overwritten.`rI want this text instead "
```

Обратите внимание, что текст перед `` `r `` символом не удаляется, он перезаписывается.

```Output
I want this text instead written.
```

## <a name="horizontal-tab-t"></a>Горизонтальная табуляция ('t)

Символ горизонтальной табуляции ( `` `t `` ) перемещается на следующую позицию табуляции и продолжит запись в этот момент. По умолчанию в консоли PowerShell имеется позиция табуляции в каждой восьмой области.

В этом примере вставляются две вкладки между каждым столбцом.

```powershell
"Column1`t`tColumn2`t`tColumn3"
```

```Output
Column1         Column2         Column3
```

## <a name="vertical-tab-v"></a>Вертикальная табуляция ("v")

Символ горизонтальной табуляции ( `` `v `` ) перемещается на следующую позицию вертикальной табуляции и записывает остальные выходные данные в этот момент. Это не влияет на консоль Windows по умолчанию.

```powershell
Write-Host "There is a vertical tab`vbetween the words."
```

В следующем примере показаны выходные данные, которые можно получить на принтере или на другом узле консоли.

```Output
There is a vertical tab
                       between the words.
```

## <a name="stop-parsing-token---"></a>Маркер отмены синтаксического анализа (--%)

Токен "Отмена синтаксического анализа" ( `--%` ) предотвращает интерпретацию строк в PowerShell как командами и выражениями PowerShell. Это позволяет передавать эти строки другим программам для интерпретации.

Поместите токен "точка-анализ" после имени программы и перед аргументами программы, которые могут вызвать ошибки.

В этом примере `Icacls` команда использует токен-синтаксический анализ.

```powershell
icacls X:\VMS --% /grant Dom\HVAdmin:(CI)(OI)F
```

PowerShell отправляет следующую строку в `Icacls` .

```
X:\VMS /grant Dom\HVAdmin:(CI)(OI)F
```

Вот еще один пример. Функция **шоваргс** выводит переданные ей значения. В этом примере мы передаем переменную с именем `$HOME` в функцию дважды.

```powershell
function showArgs {
  "`$args = " + ($args -join '|')
}

showArgs $HOME --% $HOME
```

В выходных данных можно увидеть, что для первого параметра Переменная `$HOME` интерпретируется PowerShell, чтобы значение переменной передавалось функции. Второе использование `$HOME` поступает после маркера-синтаксического анализа, поэтому строка "$Home" передается в функцию без интерпретации.

```Output
$args = C:\Users\username|--%|$HOME
```

Дополнительные сведения о токене завершения синтаксического анализа см. в разделе [about_Parsing](about_Parsing.md).

## <a name="see-also"></a>См. также статью

[about_Quoting_Rules](about_Quoting_Rules.md)