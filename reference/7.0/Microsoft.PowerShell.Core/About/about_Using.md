---
description: Позволяет указать, какие пространства имен используются в сеансе.
Locale: en-US
ms.date: 01/19/2021
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_using?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Using
ms.openlocfilehash: 2ada269fd0ce6b34a5f7faccfddf47a799301eb9
ms.sourcegitcommit: 94d597c4fb38793bc49ca7610e2c9973b1e577c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/21/2021
ms.locfileid: "98619947"
---
# <a name="about-using"></a>Об использовании

## <a name="short-description"></a>КРАТКОЕ ОПИСАНИЕ
Позволяет указать, какие пространства имен используются в сеансе.

## <a name="long-description"></a>ПОДРОБНОЕ ОПИСАНИЕ

`using`Инструкция позволяет указать, какие пространства имен используются в сеансе. Добавление пространств имен упрощает использование классов и членов .NET и позволяет импортировать классы из модулей скриптов и сборок.

`using`Операторы должны располагаться перед любыми другими инструкциями в скрипте или модуле. Ни один оператор без комментариев не может предшествовать ему, включая параметры.

`using`Инструкция не должна содержать переменных.

`using`Оператор не следует путать с `using:` модификатором области для переменных. Дополнительные сведения см. в разделе [about_Remote_Variables](about_Remote_Variables.md).

## <a name="namespace-syntax"></a>Синтаксис пространства имен

Чтобы указать пространства имен .NET, из которых следует разрешить типы:

```
using namespace <.NET-namespace>
```

Указание пространства имен упрощает ссылки на типы по их коротким именам.

## <a name="module-syntax"></a>Синтаксис модуля

Чтобы загрузить классы из модуля PowerShell, сделайте следующее:

```
using module <module-name>
```

Значением `<module-name>` может быть имя модуля, полная спецификация модуля или путь к файлу модуля.

Если `<module-name>` является путем, путь может быть полным или относительным. Относительный путь разрешается относительно скрипта, содержащего инструкцию using.

> [!NOTE]
> Если относительный путь содержит косую черту ( `/` ), PowerShell обрабатывает путь относительно текущего расположения, а не относительно расположения скрипта. Эта ошибка исправлена в PowerShell 7,1.

Если `<module-name>` является спецификацией имени или модуля, PowerShell выполняет поиск в **PSModulePath** для указанного модуля.

Спецификация модуля — это хэш-таблица, которая содержит следующие ключи.

- `ModuleName` - **Обязательное требование** Указывает имя модуля.
- `GUID` - **Необязательно** Указывает идентификатор GUID модуля.
- **Также необходимо** указать один из трех указанных ниже ключей. Эти ключи нельзя использовать совместно.
  - `ModuleVersion` — Указывает минимальную допустимую версию модуля.
  - `RequiredVersion` — Указывает точную, требуемую версию модуля.
  - `MaximumVersion` — Указывает максимально допустимую версию модуля.

`using module`Оператор импортирует классы из корневого модуля ( `ModuleToProcess` ) модуля скрипта или двоичного модуля. Он не выполняет согласованный импорт классов, определенных во вложенных модулях или классах, определенных в скриптах, которые являются точками, источником которых является модуль. Классы, которые должны быть доступны пользователям за пределами модуля, должны быть определены в корневом модуле.

Во время разработки модуля скрипта часто вносятся изменения в код, а затем загружается новая версия модуля `Import-Module` с параметром **Force** . Это применимо только к изменениям функций в корневом модуле. `Import-Module` не перезагружает вложенные модули. Кроме того, не существует способа загрузить обновленные классы.

Чтобы убедиться, что вы используете последнюю версию, необходимо выгрузить модуль с помощью `Remove-Module` командлета. `Remove-Module` Удаляет корневой модуль, все вложенные модули и все классы, определенные в модулях. Затем можно перезагрузить модуль и классы с помощью `Import-Module` и `using module` инструкции.

## <a name="assembly-syntax"></a>Синтаксис сборки

Предварительная загрузка типов из сборки .NET:

```
using assembly <.NET-assembly-path>
```

При загрузке сборки выгружаются типы .NET из этой сборки в скрипт во время синтаксического анализа. Это позволяет создавать новые классы PowerShell, использующие типы из предварительно загруженной сборки.

Если вы не создаете новые классы PowerShell, используйте `Add-Type` вместо этого командлет. Дополнительные сведения см. в разделе [Add-Type](xref:Microsoft.PowerShell.Utility.Add-Type).

## <a name="examples"></a>Примеры

### <a name="example-1---add-namespaces-for-typename-resolution"></a>Пример 1. Добавление пространств имен для разрешения имени TypeName

Следующий скрипт получает криптографический хэш для строки "Hello World".

Обратите внимание, что `using namespace System.Text` и `using namespace System.IO` упрощает ссылки на `[UnicodeEncoding]` в и и в `System.Text` `[Stream]` `[MemoryStream]` `System.IO` .

```powershell
using namespace System.Text
using namespace System.IO

[string]$string = "Hello World"
## Valid values are "SHA1", "SHA256", "SHA384", "SHA512", "MD5"
[string]$algorithm = "SHA256"

[byte[]]$stringbytes = [UnicodeEncoding]::Unicode.GetBytes($string)

[Stream]$memorystream = [MemoryStream]::new($stringbytes)
$hashfromstream = Get-FileHash -InputStream $memorystream `
  -Algorithm $algorithm
$hashfromstream.Hash.ToString()
```

### <a name="example-2---load-classes-from-a-script-module"></a>Пример 2. Загрузка классов из модуля скрипта

В этом примере у нас есть модуль скрипта PowerShell с именем **кардгамес** , который определяет следующие классы:

- **Кардгамес. колода**
- **Кардгамес. Card**

`Import-Module` и `#requires` инструкция импортирует только функции, псевдонимы и переменные модуля, как определено модулем. Классы не импортируются. `using module`Команда импортирует модуль, а также загружает определения классов.

```powershell
using module CardGames
using namespace CardGames

[Deck]$deck = [Deck]::new()
$deck.Shuffle()
[Card[]]$hand1 = $deck.Deal(5)
[Card[]]$hand2 = $deck.Deal(5)
[Card[]]$hand3 = $deck.Deal(5)
```

### <a name="example-3---load-classes-from-an-assembly"></a>Пример 3. Загрузка классов из сборки

В этом примере загружается сборка, чтобы ее классы можно было использовать для создания новых классов PowerShell. Следующий скрипт создает новый класс PowerShell, производный от класса **директориконтекст** .

```powershell
using assembly 'C:\Program Files\PowerShell\7\System.DirectoryServices.dll'
using namespace System.DirectoryServices.ActiveDirectory

class myDirectoryClass : System.DirectoryServices.ActiveDirectory.DirectoryContext
{

  [DirectoryContext]$domain

  myDirectoryClass([DirectoryContextType]$ctx) : base($ctx)
  {
    $this.domain = [DirectoryContext]::new([DirectoryContextType]$ctx)
  }

}

$myDomain = [myDirectoryClass]::new([DirectoryContextType]::Domain)
$myDomain
```

```Output
domain                                                    Name UserName ContextType
------                                                    ---- -------- -----------
System.DirectoryServices.ActiveDirectory.DirectoryContext                    Domain
```
