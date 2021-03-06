---
description: Описывает ключевое слово, которое обрабатывает завершающую ошибку.
keywords: powershell,командлет
Locale: en-US
ms.date: 06/04/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_trap?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Trap
ms.openlocfilehash: 9627c632769cb87e790cc421c09d1103b90acf1d
ms.sourcegitcommit: f874dc1d4236e06a3df195d179f59e0a7d9f8436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "93231901"
---
# <a name="about-trap"></a>О ловушке

## <a name="short-description"></a>Краткое описание

Описывает ключевое слово, которое обрабатывает завершающую ошибку.

## <a name="long-description"></a>Подробное описание

Завершающая ошибка останавливает выполнение инструкции. Если PowerShell каким-либо образом не обрабатывает завершающую ошибку, PowerShell также прекращает выполнение функции или скрипта в текущем конвейере. На других языках, таких как C#, завершающие ошибки называются исключениями.

`trap`Ключевое слово указывает список инструкций, выполняемых при возникновении неустранимой ошибки. `trap` операторы обработают завершающие ошибки следующими способами:

- Отобразить ошибку после обработки `trap` блока инструкций и продолжить выполнение скрипта или функции, содержащей `trap` . Это поведение по умолчанию.

- Отображение ошибки и прерывание выполнения скрипта или функции, содержащей `trap` оператор using, `break` в `trap` инструкции.

- Это приведет к ошибке, но продолжить выполнение скрипта или функции, содержащей, `trap` с помощью `continue` `trap` инструкции в операторе.

Список инструкций `trap` может включать несколько условий или вызовов функций. `trap`Может записывать журналы, условия теста или даже запускать другую программу.

### <a name="syntax"></a>Синтаксис

`trap`Оператор имеет следующий синтаксис:

```powershell
trap [[<error type>]] {<statement list>}
```

`trap`Инструкция включает список инструкций, которые выполняются при возникновении неустранимой ошибки. `trap`Оператор состоит из `trap` ключевого слова, при необходимости за которым следует выражение типа, и блок инструкций, содержащий список инструкций, которые выполняются при перехвате ошибки. Выражение типа Уточнение типов ошибок, которые `trap` перехватываются.

Сценарий или команда может иметь несколько `trap` инструкций. `trap` операторы могут находиться в любом месте скрипта или команды.

### <a name="trapping-all-terminating-errors"></a>Перехват всех завершающих ошибок

При возникновении завершающей ошибки, которая не обрабатывается другим способом в скрипте или команде, PowerShell проверяет наличие `trap` инструкции, обрабатывающей ошибку. Если указан `trap` оператор, PowerShell продолжит выполнение скрипта или команды в `trap` инструкции.

Ниже приведен пример очень простой `trap` инструкции:

```powershell
trap {"Error found."}
```

Эта `trap` инструкция захватывает все завершающие ошибки.

В следующем примере функция включает строку серьезные, которая вызывает ошибку времени выполнения.

```powershell
function TrapTest {
    trap {"Error found."}
    nonsenseString
}

TrapTest
```

При выполнении этой функции возвращается следующее:

```Output
Error found.
nonsenseString : The term 'nonsenseString' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.
At line:3 char:5
+     nonsenseString
+     ~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (nonsenseString:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

Следующий пример включает `trap` инструкцию, которая отображает ошибку с помощью `$_` автоматической переменной:

```powershell
function TrapTest {
    trap {"Error found: $_"}
    nonsenseString
}

TrapTest
```

При выполнении этой версии функции возвращается следующее:

```Output
Error found: The term 'nonsenseString' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
nonsenseString : The term 'nonsenseString' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.
At line:3 char:5
+     nonsenseString
+     ~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (nonsenseString:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

> [!IMPORTANT]
> `trap` операторы могут быть определены в любом месте заданной области, но всегда применяются ко всем операторам в этой области. Во время выполнения `trap` инструкции в блоке определяются до выполнения других инструкций. В JavaScript это называется [поднятием](https://wikipedia.org/wiki/JavaScript_syntax#hoisting). Это означает, что `trap` инструкции применяются ко всем операторам в этом блоке, даже если выполнение не было расширено до точки, в которой они определены. Например, определение в `trap` конце скрипта и выдача ошибки в первой инструкции все еще активирует это `trap` .

### <a name="trapping-specific-errors"></a>Перехват конкретных ошибок

Сценарий или команда может иметь несколько `trap` инструкций. `trap`Можно определить для обработки определенных ошибок.

В следующем примере показана `trap` инструкция, которая перехватывает определенную ошибку **комманднотфаундексцептион** :

```powershell
trap [System.Management.Automation.CommandNotFoundException]
    {"Command error trapped"}
```

Если функция или скрипт встречает строку, которая не соответствует известной команде, эта `trap` инструкция выводит строку "Перехват ошибки команды".
После выполнения `trap` списка инструкций PowerShell записывает объект ошибки в поток ошибок, а затем возобновляет выполнение скрипта.

PowerShell использует типы исключений .NET. В следующем примере задается тип ошибки **System. Exception** :

```powershell
trap [System.Exception] {"An error trapped"}
```

Тип ошибки **комманднотфаундексцептион** наследуется от типа **System. Exception** . Эта инструкция захватывает ошибку, созданную неизвестной командой. Он также выполняет треппинг других типов ошибок.

В скрипте может быть несколько `trap` операторов. Каждый тип ошибки может быть перехвачен только одной `trap` инструкцией. При возникновении неустранимой ошибки PowerShell ищет объект `trap` с наиболее конкретным совпадением, начиная с текущей области выполнения.

Следующий пример скрипта содержит ошибку. Скрипт включает в себя общий `trap` оператор, который захватывает все завершающие ошибки и определенную `trap` инструкцию, указывающую тип **комманднотфаундексцептион** .

```powershell
trap {"Other terminating error trapped" }
trap [System.Management.Automation.CommandNotFoundException] {
  "Command error trapped"
}
nonsenseString
```

Выполнение этого скрипта приводит к следующему результату:

```Output
Command error trapped
nonsenseString : The term 'nonsenseString' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.
At C:\Temp\traptest.ps1:5 char:1
+ nonsenseString
+ ~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (nonsenseString:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

Так как PowerShell не распознает "Нонсенсестринг" как командлет или другой элемент, он возвращает ошибку **комманднотфаундексцептион** . Эта завершающая ошибка захватывается конкретной `trap` инструкцией.

Следующий пример скрипта содержит те же `trap` инструкции с другой ошибкой:

```powershell
trap {"Other terminating error trapped" }
trap [System.Management.Automation.CommandNotFoundException]
    {"Command error trapped"}
1/$null
```

Выполнение этого скрипта приводит к следующему результату:

```Output
Attempted to divide by zero.
At C:\temp\traptest.ps1:4 char:1
+ 1/$null
+ ~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], RuntimeException
    + FullyQualifiedErrorId : RuntimeException
```

Попытка деления на ноль не приводит к созданию ошибки **комманднотфаундексцептион** . Вместо этого эта ошибка перехвачена другой `trap` инструкцией, которая перехватывает все завершающие ошибки.

### <a name="trapping-errors-and-scope"></a>Перехват ошибок и области действия

Если завершающая ошибка возникает в той же области, что и `trap` инструкция, то PowerShell выполняет список инструкций, определенных `trap` . Выполнение продолжится в операторе после ошибки. Если `trap` инструкция находится в области, отличной от ошибки, выполнение переходит к следующему оператору, который находится в той же области, что и `trap` инструкция.

Например, если в функции возникает ошибка, а `trap` оператор находится в функции, скрипт переходит к следующему оператору. Следующий скрипт содержит ошибку и `trap` инструкцию:

```powershell
function function1 {
    trap { "An error: " }
    NonsenseString
    "function1 was completed"
}

function1
```

Выполнение этого скрипта приводит к следующему результату:

```Output
An error:
NonsenseString : The term 'NonsenseString' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.
At line:3 char:5
+     NonsenseString
+     ~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (NonsenseString:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

function1 was completed
```

`trap`Инструкция в функции перехватывает ошибку. После отображения сообщения PowerShell возобновляет выполнение функции. Обратите внимание, что `Function1` выполнено.

Сравните это со следующим примером, который содержит ту же ошибку и `trap` оператор. В этом примере `trap` оператор выполняется за пределами функции:

```powershell
function function2 {
    NonsenseString
    "function2 was completed"
}

trap { "An error: " }

function2
```

Выполнение `Function2` функции приведет к следующему результату:

```Output
An error:
NonsenseString : The term 'NonsenseString' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was
included, verify that the path is correct and try again.
At C:\temp\traptest.ps1:2 char:5
+     NonsenseString
+     ~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (NonsenseString:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

В этом примере команда "функция2 WAS" не была выполнена. В обоих примерах завершающая ошибка возникает в функции. Однако в этом примере `trap` оператор находится за пределами функции. PowerShell не выполняет возврат в функцию после `trap` выполнения инструкции.

> [!CAUTION]
> Если для одного и того же условия ошибки определено несколько ловушек, `trap` используется первая определенная лексическая (самая высокая в области).

В следующем примере `trap` выполняется только с параметром "whoops 1".

```powershell
Remove-Item -ErrorAction Stop ThisFileDoesNotExist
trap { "whoops 1"; continue }
trap { "whoops 2"; continue }
```

> [!IMPORTANT]
> Оператор Trap ограничивает область, в которой она компилируется. Если у вас есть `trap` оператор внутри функции или скрипта с точкой, находящегося в исходной среде, то при выходе из функции или сценария с источником точки все `trap` инструкции внутри удаляются.

### <a name="using-the-break-and-continue-keywords"></a>Использование ключевых слов BREAK и Continue

Можно использовать `break` `continue` Ключевые слова и в инструкции, `trap` чтобы определить, продолжится ли выполнение скрипта или команды после завершающей ошибки.

Если включить `break` инструкцию в `trap` список операторов, PowerShell остановит функцию или скрипт. В следующем примере функции используется `break` ключевое слово в `trap` операторе:

```powershell
function break_example {
    trap {
        "Error trapped"
        break
    }
    1/$null
    "Function completed."
}

break_example
```

```Output
Error trapped
Attempted to divide by zero.
At line:6 char:5
+     1/$null
+     ~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : RuntimeException
```

Так как `trap` инструкция включала `break` ключевое слово, она не запускается, а строка "функция завершена" не выполняется.

Если включить `continue` в инструкцию ключевое слово `trap` , PowerShell возобновит работу после инструкции, которая вызвала ошибку, так же, как если бы она не была `break` `continue` . Однако при использовании `continue` ключевого слова PowerShell не записывает ошибку в поток ошибок.

В следующем примере функции используется `continue` ключевое слово в `trap` операторе:

```powershell
function continue_example {
    trap {
        "Error trapped"
        continue
    }
    1/$null
    "Function completed."
}

continue_example
```

```Output
Error trapped
Function completed.
```

Функция возобновляется после перехвата ошибки и выполнения инструкции function Completed. Ошибки в потоке ошибок не записываются.

## <a name="notes"></a>Примечания

`trap` операторы предоставляют простой способ для широкого обеспечения обработки всех завершающих ошибок в области. Для более детализированной обработки ошибок используйте `try` / `catch` блоки, в которых ловушки определяются с помощью `catch` инструкций. `catch`Инструкции применяются только к коду внутри связанной `try` инструкции. Дополнительные сведения см. в разделе [about_Try_Catch_Finally](about_Try_Catch_Finally.md).

## <a name="see-also"></a>См. также статью

[about_Break](about_Break.md)

[about_Continue](about_Continue.md)

[about_Scopes](about_Scopes.md)

[about_Throw](about_Throw.md)

[about_Try_Catch_Finally](about_Try_Catch_Finally.md)
