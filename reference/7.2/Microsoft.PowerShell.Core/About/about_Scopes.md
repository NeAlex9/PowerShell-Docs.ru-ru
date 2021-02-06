---
description: Объясняет концепцию Scope в PowerShell и показывает, как устанавливать и изменять область элементов.
Locale: en-US
ms.date: 11/04/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_scopes?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_scopes
ms.openlocfilehash: c9439412ab80eee4cedc1265a3927a274547d409
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "99604052"
---
# <a name="about-scopes"></a>Сведения об областях

## <a name="short-description"></a>Краткое описание
Объясняет концепцию Scope в PowerShell и показывает, как устанавливать и изменять область элементов.

## <a name="long-description"></a>Подробное описание

PowerShell защищает доступ к переменным, псевдонимам, функциям и дискам PowerShell (Псдривес), ограничивая место для чтения и изменения. PowerShell использует правила области, чтобы предотвратить случайное изменение элемента, который не должен изменяться.

Ниже приведены основные правила области.

- Области могут быть вложенными. Внешняя область называется родительской областью. Все вложенные области являются дочерними областями этого родителя.

- Элемент отображается в области, в которой он был создан, и во всех дочерних областях, если вы явно не сделаете его частным. Вы можете разместить переменные, псевдонимы, функции или диски PowerShell в одной или нескольких областях.

- Элемент, созданный в области, может быть изменен только в той области, в которой она была создана, если только вы явно не указали другую область.

При создании элемента в области и его имени вместе с элементом в другой области исходный элемент может быть скрыт под новым элементом, но не переопределен или не изменен.

## <a name="powershell-scopes"></a>Области PowerShell

PowerShell поддерживает следующие области:

- Global — область, которая действует при запуске PowerShell или при создании нового сеанса или пространства выполнения. Переменные и функции, которые имеются при запуске PowerShell в глобальной области, такие как автоматические переменные и привилегированные переменные. Переменные, псевдонимы и функции в профилях PowerShell также создаются в глобальной области. Глобальная область — это корневая родительская область в сеансе.

- Local: текущая область. Локальная область может быть глобальной или любой другой областью.

- Скрипт: область, созданная во время выполнения файла скрипта. В области скрипта выполняются только команды в скрипте. Для команд в скрипте областью скрипта является локальная область.

> [!NOTE]
> **Частный** не является областью. Это [параметр](#private-option) , который изменяет видимость элемента за пределами области, в которой определен элемент.

## <a name="parent-and-child-scopes"></a>Родительские и дочерние области

Новую дочернюю область можно создать путем вызова скрипта или функции. Вызывающая область является родительской областью. Вызываемый скрипт или функция является дочерней областью.
Вызываемые функции или скрипты могут вызывать другие функции, создавая иерархию дочерних областей, корневая область которых является глобальной областью.

Если явно не сделать элементы закрытыми, элементы в родительской области становятся доступными для дочерней области. Однако элементы, создаваемые и изменяемые в дочерней области, не влияют на родительскую область, если только при создании элементов не будет явно задана область.

> [!NOTE]
> Функции из модуля не выполняются в дочерней области вызывающей области.
> Модули имеют собственное состояние сеанса, связанное с глобальной областью.
> Весь код модуля выполняется в иерархии областей, относящихся к конкретному модулю, имеющей собственную корневую область.

## <a name="inheritance"></a>Наследование

Дочерняя область не наследует переменные, псевдонимы и функции из родительской области. Если элемент не является частным, дочерняя область может просматривать элементы в родительской области. Кроме того, он может изменить элементы, явно указав родительскую область, но элементы не являются частью дочерней области.

Однако дочерняя область создается с набором элементов. Как правило, он включает все псевдонимы с параметром **AllScope** . Этот параметр обсуждается далее в этой статье. Он включает все переменные с параметром **AllScope** , а также некоторые автоматические переменные.

Чтобы найти элементы в определенной области, используйте параметр Scope в `Get-Variable` или `Get-Alias` .

Например, чтобы получить все переменные в локальной области, введите:

```powershell
Get-Variable -Scope local
```

Чтобы получить все переменные в глобальной области, введите:

```powershell
Get-Variable -Scope global
```

## <a name="scope-modifiers"></a>Модификаторы области

Имя переменной, псевдонима или функции может содержать один из следующих необязательных модификаторов области:

- `global:` — Указывает, что имя существует в **глобальной** области.
- `local:` — Указывает, что имя существует в **локальной** области. Текущая область всегда является **локальной** .
- `private:` — Указывает, что имя является **частным** и видимым только для текущей области.
- `script:` — Указывает, что имя существует в области **скрипта** .
  Область **скрипта** является ближайшим областью файла скрипта-предка или **глобальным** , если не существует ближайшего файла скрипта-предка.
- `using:` — Используется для доступа к переменным, определенным в другой области, при выполнении скриптов с помощью таких командлетов `Start-Job` , как и `Invoke-Command` .
- `workflow:` — Указывает, что имя существует в рабочем процессе. Примечание. рабочие процессы не поддерживаются в PowerShell Core.
- `<variable-namespace>` — Модификатор, созданный поставщиком PSDrive PowerShell.
  Пример:

  |  Пространство имен  |                    Описание                     |
  | ----------- | -------------------------------------------------- |
  | `Alias:`    | Псевдонимы, определенные в текущей области               |
  | `Env:`      | Переменные среды, определенные в текущей области |
  | `Function:` | Функции, определенные в текущей области             |
  | `Variable:` | Переменные, определенные в текущей области             |

По умолчанию для скриптов используется область скрипта. Областью действия по умолчанию для функций и псевдонимов является локальная область, даже если они определены в скрипте.

### <a name="using-scope-modifiers"></a>Использование модификаторов области

Чтобы указать область новой переменной, псевдонима или функции, используйте модификатор области.

Синтаксис модификатора области в переменной:

```
$[<scope-modifier>:]<name> = <value>
```

Синтаксис модификатора области в функции:

```
function [<scope-modifier>:]<name> {<function-body>}
```

Следующая команда, не использующая модификатор области, создает переменную в текущей или **локальной** области:

```powershell
$a = "one"
```

Чтобы создать ту же переменную в **глобальной** области, используйте модификатор scope `global:` :

```powershell
$global:a = "one"
```

Чтобы создать ту же переменную в области **скрипта** , используйте `script:` Модификатор scope:

```powershell
$script:a = "one"
```

Кроме того, можно использовать модификатор области с функциями. Следующее определение функции создает функцию в **глобальной** области видимости:

```powershell
function global:Hello {
  Write-Host "Hello, World"
}
```

Кроме того, можно использовать модификаторы области для ссылки на переменную в другой области.
Следующая команда ссылается на `$test` переменную, сначала в локальной области, а затем в глобальной области:

```powershell
$test
$global:test
```

### <a name="the-using-scope-modifier"></a>`Using:`Модификатор области видимости

Использование — это специальный модификатор области, который определяет локальную переменную в удаленной команде. Без модификатора PowerShell требует, чтобы переменные в удаленных командах были определены в удаленном сеансе.

`Using`Модификатор области представлен в PowerShell 3,0.

Для любого скрипта или команды, выполняемой вне сеанса, необходим `Using` Модификатор области для внедрения значений переменных из области вызывающего сеанса, чтобы код сеанса мог получить к ним доступ. `Using`Модификатор области поддерживается в следующих контекстах:

- Удаленно выполненные команды, запущенные с `Invoke-Command` использованием параметров **ComputerName**, **HostName**, **сшконнектион** или **Session** (удаленный сеанс)
- Фоновые задания, запущенные с помощью `Start-Job` (вне процесса)
- Задания потоков, запущенные через `Start-ThreadJob` или `ForEach-Object -Parallel` (отдельный сеанс потока)

В зависимости от контекста значения внедренных переменных — это либо независимые копии данных в области вызывающего объекта, либо ссылки на него. В удаленных и необработанных сеансах они всегда являются независимыми копиями.

Дополнительные сведения см. в разделе [about_Remote_Variables](about_Remote_Variables.md).

В сеансах потока они передаются по ссылке. Это означает, что переменные области вызовов можно изменять в другом потоке. Для безопасного изменения переменных требуется синхронизация потоков.

Дополнительные сведения см. в разделах:

- [Start-ThreadJob](xref:ThreadJob.Start-ThreadJob)
- [ForEach-Object](xref:Microsoft.PowerShell.Core.ForEach-Object)

#### <a name="serialization-of-variable-values"></a>Сериализация значений переменных

Удаленные команды и фоновые задания выполняются вне процесса.
Необработанные сеансы используют сериализацию и десериализацию на основе XML, чтобы сделать значения переменных доступными через границы процесса. Процесс сериализации преобразует объекты в **PSObject** , который содержит исходные свойства объектов, но не его методы.

Для ограниченного набора типов десериализация восстанавливает объекты обратно в исходный тип. Восстановленный объект является копией исходного экземпляра объекта.
Он содержит свойства и методы типа. Для простых типов, таких как **System. Version**, копия является точной. Для сложных типов копия — неидеальны. Например, rehydratя объектов сертификатов не включает закрытый ключ.

Экземпляры всех остальных типов являются экземплярами **PSObject** . Свойство **PSTypeNames** содержит имя исходного типа с префиксом **десериализации**, например **Deserialized.SysTEM. Data. DataTable**

### <a name="the-allscope-option"></a>Параметр AllScope

Переменные и псевдонимы имеют свойство **Option** , которое может принимать значение **AllScope**. Элементы, имеющие свойство **AllScope** , становятся частью любых создаваемых дочерних областей, хотя они не задним числом наследуются родительскими областями.

Элемент, имеющий свойство **AllScope** , отображается в дочерней области и является частью этой области. Изменения элемента в любой области влияют на все области, в которых определена переменная.

### <a name="managing-scope"></a>Управление областью

Несколько командлетов имеют параметр **области** , который позволяет получать или задавать (создавать и изменять) элементы в определенной области. Используйте следующую команду, чтобы найти все командлеты в сеансе с параметром **области** :

```powershell
Get-Help * -Parameter scope
```

Чтобы найти переменные, видимые в определенной области, используйте `Scope` параметр `Get-Variable` . Видимые переменные включают в себя глобальные переменные, переменные в родительской области и переменные в текущей области.

Например, следующая команда получает переменные, видимые в локальной области:

```powershell
Get-Variable -Scope local
```

Чтобы создать переменную в определенной области, используйте модификатор области или параметр **Scope** в `Set-Variable` . Следующая команда создает переменную в глобальной области видимости:

```powershell
New-Variable -Scope global -Name a -Value "One"
```

Для указания области можно также использовать параметр scope `New-Alias` `Set-Alias` командлетов, или `Get-Alias` . Следующая команда создает псевдоним в глобальной области:

```powershell
New-Alias -Scope global -Name np -Value Notepad.exe
```

Чтобы получить функции в определенной области, используйте `Get-Item` командлет в области. `Get-Item`Командлет не имеет параметра **области** .

> [!NOTE]
> Для командлетов, использующих параметр **области** , можно также ссылаться на области по числу. Число описывает относительное расположение одной области в другую. Область 0 представляет текущую или локальную область. Область 1 указывает непосредственную родительскую область. Область 2 указывает родителя родительской области и т. д. Пронумерованные области полезны, если создано много рекурсивных областей.

### <a name="using-dot-source-notation-with-scope"></a>Использование нотации источника точки с областью видимости

Сценарии и функции соответствуют всем правилам области. Они создаются в определенной области и влияют только на эту область, если только не используется параметр командлета или модификатор области для изменения этой области.

Однако можно добавить скрипт или функцию в текущую область с помощью точечной нотации источника. Затем, когда сценарий выполняется в текущей области, все функции, псевдонимы и переменные, создаваемые сценарием, доступны в текущей области.

Чтобы добавить функцию в текущую область, введите точку (.) и пробел перед путем и именем функции в вызове функции.

Например, чтобы запустить скрипт Sample.ps1 из каталога C:\Scripts в области скрипта (по умолчанию для сценариев), используйте следующую команду:

```powershell
c:\scripts\sample.ps1
```

Чтобы запустить скрипт Sample.ps1 в локальной области, используйте следующую команду:

```powershell
. c:\scripts.sample.ps1
```

При использовании оператора Call (&) для выполнения функции или скрипта он не добавляется в текущую область. В следующем примере используется оператор Call:

```powershell
& c:\scripts.sample.ps1
```

Дополнительные сведения о операторе Call можно узнать в [about_operators](about_operators.md).

Любые псевдонимы, функции или переменные, создаваемые сценарием Sample.ps1, недоступны в текущей области.

## <a name="restricting-without-scope"></a>Ограничение без области

Несколько концепций PowerShell похожи на область или взаимодействуют с областью действия. Эти понятия можно путать с областью действия или поведением области.

Сеансы, модули и вложенные запросы являются автономными средами, но они не являются дочерними областями глобальной области в сеансе.

### <a name="sessions"></a>Сеансы

Сеанс — это среда, в которой выполняется PowerShell. При создании сеанса на удаленном компьютере PowerShell устанавливает постоянное подключение к удаленному компьютеру. Постоянное подключение позволяет использовать сеанс для нескольких связанных команд.

Поскольку сеанс является автономной средой, он имеет собственную область, но сеанс не является дочерней областью сеанса, в котором он был создан. Сеанс начинается с собственной глобальной области. Эта область не зависит от глобальной области действия сеанса. В сеансе можно создать дочерние области. Например, можно выполнить сценарий для создания дочерней области в сеансе.

### <a name="modules"></a>Модули

Вы можете использовать модуль PowerShell для совместного использования и доставки средств PowerShell. Модуль — это единица, которая может содержать командлеты, скрипты, функции, переменные, псевдонимы и другие полезные элементы. Если явно не определено, элементы в модуле недоступны за пределами модуля. Таким образом, можно добавить модуль в сеанс и использовать открытые элементы, не заботясь о том, что другие элементы могут переопределять командлеты, сценарии, функции и другие элементы в сеансе.

По умолчанию модули загружаются в верхний уровень текущего _состояния сеанса_ , а не в текущую _область_. Текущее состояние сеанса может быть состоянием сеанса модуля или глобальным состоянием сеанса. Добавление модуля в сеанс не приводит к изменению области. Если вы используете глобальную область, модули загружаются в глобальное состояние сеанса. Все операции экспорта помещаются в глобальные таблицы.
При загрузке _Module2 из Module1_ Module2 загружается в состояние сеанса Module1, а не в глобальное состояние сеанса. Все операции экспорта из Module2 размещаются в верхней части состояния сеанса Module1. Если используется `Import-Module -Scope local` , то экспорты помещаются в текущий объект области, а не на верхний уровень. Если вы используете _модуль_ и используете `Import-Module -Scope global` (или `Import-Module -Global` ) для загрузки другого модуля, этот модуль и его экспорты загружаются в глобальное состояние сеанса, а не в локальное состояние сеанса модуля. Эта функция предназначена для написания модуля, который управляет модулями. Модуль **виндовскомпатибилити** выполняет это для импорта прокси-модулей в глобальное состояние сеанса.

В состоянии сеанса модули имеют собственную область действия. Рассмотрим следующий модуль `C:\temp\mod1.psm1` :

```powershell
$a = "Hello"

function foo {
    "`$a = $a"
    "`$global:a = $global:a"
}
```

Теперь создадим глобальную переменную `$a` , присвойте ей значение и вызовите функцию **foo**.

```powershell
$a = "Goodbye"
foo
```

Модуль объявляет переменную `$a` в области модуля, а функция **foo** выводит значение переменной в обеих областях.

```Output
$a = Hello
$global:a = Goodbye
```

### <a name="nested-prompts"></a>Вложенные запросы

Вложенные запросы не имеют собственной области. При вводе вложенного запроса вложенный запрос является подмножеством среды. Но остается в локальной области.

Скрипты имеют собственную область действия. При отладке скрипта и достижении точки останова в скрипте необходимо ввести область скрипта.

### <a name="private-option"></a>Частный вариант

Псевдонимы и переменные имеют свойство **Option** , которое может принимать значение **Private**. Элементы с **закрытым** параметром можно просматривать и изменять в области, в которой они создаются, но их нельзя просматривать или изменять вне этой области.

Например, если вы создаете переменную с частным параметром в глобальной области, а затем выполняете сценарий, `Get-Variable` команды в скрипте не отображают закрытую переменную. Использование модификатора глобальной области в этом экземпляре не приводит к отображению закрытой переменной.

Можно использовать параметр Option `New-Variable` `Set-Variable` `New-Alias` командлетов,,, и, `Set-Alias` чтобы задать для свойства параметра значение Private.

### <a name="visibility"></a>Видимость

Свойство **видимости** переменной или псевдонима определяет, можно ли видеть элемент за пределами контейнера, в котором он был создан. Контейнером может быть модуль, сценарий или оснастка. Видимость предназначена для контейнеров так же, как и **закрытое** значение свойства **Option** для областей.

Свойство **Visibility** принимает **открытые** и **закрытые** значения. Элементы, имеющие закрытую видимость, можно просматривать и изменять только в контейнере, в котором они были созданы. Если контейнер добавлен или импортирован, элементы, имеющие закрытую видимость, не могут быть просмотрены или изменены.

Поскольку видимость предназначена для контейнеров, она работает по-разному в области.

- При создании элемента с закрытой видимостью в глобальной области нельзя просматривать или изменять элемент в какой бы то ни было области.
- При попытке просмотра или изменения значения переменной, имеющей закрытую видимость, PowerShell возвращает сообщение об ошибке.

`New-Variable` `Set-Variable` Для создания переменной с закрытой видимостью можно использовать командлеты и.

## <a name="examples"></a>Примеры

### <a name="example-1-change-a-variable-value-only-in-a-script"></a>Пример 1. изменение значения переменной только в скрипте

Следующая команда изменяет значение `$ConfirmPreference` переменной в скрипте. Изменение не влияет на глобальную область.

Сначала для вывода значения `$ConfirmPreference` переменной в локальной области используйте следующую команду:

```
PS>  $ConfirmPreference
High
```

Создайте скрипт Scope.ps1, который содержит следующие команды:

```powershell
$ConfirmPreference = "Low"
"The value of `$ConfirmPreference is $ConfirmPreference."
```

Выполните скрипт. Скрипт изменяет значение `$ConfirmPreference` переменной, а затем сообщает свое значение в области скрипта. Выходные данные должны выглядеть следующим образом:

```output
The value of $ConfirmPreference is Low.
```

Затем проверьте текущее значение `$ConfirmPreference` переменной в текущей области.

```
PS>  $ConfirmPreference
High
```

В этом примере показано, что изменения значения переменной в области скрипта не влияют на значение переменной в родительской области.

### <a name="example-2-view-a-variable-value-in-different-scopes"></a>Пример 2. Просмотр значения переменной в разных областях

Модификаторы области можно использовать для просмотра значения переменной в локальной области и в родительской области.

Сначала определите `$test` переменную в глобальной области.

```powershell
$test = "Global"
```

Затем создайте скрипт Sample.ps1, определяющий `$test` переменную. В скрипте используйте модификатор области для ссылки на глобальную или локальную версию `$test` переменной.

В Sample.ps1:

```powershell
$test = "Local"
"The local value of `$test is $test."
"The global value of `$test is $global:test."
```

При запуске Sample.ps1 выходные данные должны выглядеть следующим образом:

```output
The local value of $test is Local.
The global value of $test is Global.
```

По завершении скрипта `$test` в сеансе определяется только глобальное значение.

```
PS>  $test
Global
```

### <a name="example-3-change-the-value-of-a-variable-in-a-parent-scope"></a>Пример 3. изменение значения переменной в родительской области

Если вы не защищаете элемент с помощью параметра private или другого метода, то можете просмотреть и изменить значение переменной в родительской области.

Сначала определите `$test` переменную в глобальной области.

```powershell
$test = "Global"
```

Затем создайте скрипт Sample.ps1, определяющий `$test` переменную. В скрипте используйте модификатор области для ссылки на глобальную или локальную версию `$test` переменной.

В Sample.ps1:

```powershell
$global:test = "Local"
"The global value of `$test is $global:test."
```

По завершении скрипта изменяется глобальное значение `$test` .

```
PS>  $test
Local
```

### <a name="example-4-creating-a-private-variable"></a>Пример 4. Создание закрытой переменной

Частная переменная — это переменная, которая имеет свойство **Option** со значением *Private*. *Закрытые* переменные наследуются дочерней областью, но их можно просматривать или изменять только в области, в которой они были созданы.

Следующая команда создает закрытую переменную с именем `$ptest` в локальной области.

```powershell
New-Variable -Name ptest -Value 1 -Option private
```

Можно отобразить и изменить значение `$ptest` в локальной области.

```
PS>  $ptest
1

PS>  $ptest = 2
PS>  $ptest
2
```

Затем создайте скрипт Sample.ps1, содержащий следующие команды. Команда пытается отобразить и изменить значение `$ptest` .

В Sample.ps1:

```powershell
"The value of `$Ptest is $Ptest."
"The value of `$Ptest is $global:Ptest."
```

`$ptest`Переменная не видна в области скрипта, выходные данные пусты.

```powershell
"The value of $Ptest is ."
"The value of $Ptest is ."
```

### <a name="example-5-using-a-local-variable-in-a-remote-command"></a>Пример 5. Использование локальной переменной в удаленной команде

Для переменных в удаленной команде, созданной в локальном сеансе, используйте `Using` Модификатор области. В PowerShell предполагается, что переменные в удаленных командах были созданы в удаленном сеансе.

Синтаксис:

```
$Using:<VariableName>
```

Например, следующие команды создают `$Cred` переменную в локальном сеансе, а затем используют эту `$Cred` переменную в удаленной команде:

```powershell
$Cred = Get-Credential
Invoke-Command $s {Remove-Item .\Test*.ps1 -Credential $Using:Cred}
```

Область использования была введена в PowerShell 3,0. В PowerShell 2,0, чтобы указать, что переменная была создана в локальном сеансе, используйте следующий формат команды.

```powershell
$Cred = Get-Credential
Invoke-Command $s {
  param($c)
  Remove-Item .\Test*.ps1 -Credential $c
} -ArgumentList $Cred
```

## <a name="see-also"></a>См. также

[about_Variables](about_Variables.md)

[about_Environment_Variables](about_Environment_Variables.md)

[about_Functions](about_Functions.md)

[about_Script_Blocks](about_Script_Blocks.md)

[Start-ThreadJob](/powershell/module/ThreadJob/Start-ThreadJob)