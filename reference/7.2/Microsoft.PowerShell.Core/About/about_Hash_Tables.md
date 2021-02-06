---
description: Описывает создание, использование и сортировку хэш-таблиц в PowerShell.
Locale: en-US
ms.date: 11/28/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Hash_Tables
ms.openlocfilehash: dec2683acfa4fcf79419beea9e0840387d3d43d1
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "99599787"
---
# <a name="about-hash-tables"></a><span data-ttu-id="c6dce-103">О хэш-таблицах</span><span class="sxs-lookup"><span data-stu-id="c6dce-103">About Hash Tables</span></span>

## <a name="short-description"></a><span data-ttu-id="c6dce-104">КРАТКОЕ ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="c6dce-104">SHORT DESCRIPTION</span></span>
<span data-ttu-id="c6dce-105">Описывает создание, использование и сортировку хэш-таблиц в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6dce-105">Describes how to create, use, and sort hash tables in PowerShell.</span></span>

## <a name="long-description"></a><span data-ttu-id="c6dce-106">ПОДРОБНОЕ ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="c6dce-106">LONG DESCRIPTION</span></span>

<span data-ttu-id="c6dce-107">Хэш-таблица, также называемая словарем или ассоциативным массивом, представляет собой компактную структуру данных, в которой хранится одна или несколько пар "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="c6dce-107">A hash table, also known as a dictionary or associative array, is a compact data structure that stores one or more key/value pairs.</span></span> <span data-ttu-id="c6dce-108">Например, хэш-таблица может содержать ряд IP-адресов и имен компьютеров, где IP-адреса являются ключами, а имена компьютеров — значениями, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="c6dce-108">For example, a hash table might contain a series of IP addresses and computer names, where the IP addresses are the keys and the computer names are the values, or vice versa.</span></span>

<span data-ttu-id="c6dce-109">В PowerShell каждая хэш-таблица является объектом Hashtable (System. Collections. Hashtable).</span><span class="sxs-lookup"><span data-stu-id="c6dce-109">In PowerShell, each hash table is a Hashtable (System.Collections.Hashtable) object.</span></span> <span data-ttu-id="c6dce-110">В PowerShell можно использовать свойства и методы объектов Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c6dce-110">You can use the properties and methods of Hashtable objects in PowerShell.</span></span>

<span data-ttu-id="c6dce-111">Начиная с PowerShell 3,0, можно использовать атрибут [ordered] для создания упорядоченного словаря (System. Collections. специализированные. Ордереддиктионари) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6dce-111">Beginning in PowerShell 3.0, you can use the [ordered] attribute to create an ordered dictionary (System.Collections.Specialized.OrderedDictionary) in PowerShell.</span></span>

<span data-ttu-id="c6dce-112">Упорядоченные словари отличаются от хэш-таблиц тем, что ключи всегда отображаются в порядке их перечисления.</span><span class="sxs-lookup"><span data-stu-id="c6dce-112">Ordered dictionaries differ from hash tables in that the keys always appear in the order in which you list them.</span></span> <span data-ttu-id="c6dce-113">Порядок ключей в хэш-таблице не определен.</span><span class="sxs-lookup"><span data-stu-id="c6dce-113">The order of keys in a hash table is not determined.</span></span>

<span data-ttu-id="c6dce-114">Ключи и значение в хэш-таблицах также являются объектами .NET.</span><span class="sxs-lookup"><span data-stu-id="c6dce-114">The keys and value in hash tables are also .NET objects.</span></span> <span data-ttu-id="c6dce-115">Чаще всего это строки или целые числа, но они могут иметь любой тип объекта.</span><span class="sxs-lookup"><span data-stu-id="c6dce-115">They are most often strings or integers, but they can have any object type.</span></span> <span data-ttu-id="c6dce-116">Также можно создать вложенные хэш-таблицы, в которых значение ключа является другой хэш-таблицей.</span><span class="sxs-lookup"><span data-stu-id="c6dce-116">You can also create nested hash tables, in which the value of a key is another hash table.</span></span>

<span data-ttu-id="c6dce-117">Хэш-таблицы часто используются, так как они очень эффективны для поиска и извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="c6dce-117">Hash tables are frequently used because they are very efficient for finding and retrieving data.</span></span> <span data-ttu-id="c6dce-118">Хэш-таблицы можно использовать для хранения списков и создания вычисляемых свойств в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6dce-118">You can use hash tables to store lists and to create calculated properties in PowerShell.</span></span> <span data-ttu-id="c6dce-119">И PowerShell имеет командлет ConvertFrom-StringData, который преобразует строки в хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c6dce-119">And, PowerShell has a cmdlet, ConvertFrom-StringData, that converts strings to a hash table.</span></span>

### <a name="syntax"></a><span data-ttu-id="c6dce-120">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c6dce-120">Syntax</span></span>

<span data-ttu-id="c6dce-121">Синтаксис хэш-таблицы выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6dce-121">The syntax of a hash table is as follows:</span></span>

```powershell
@{ <name> = <value>; [<name> = <value> ] ...}
```

<span data-ttu-id="c6dce-122">Синтаксис упорядоченного словаря выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6dce-122">The syntax of an ordered dictionary is as follows:</span></span>

```powershell
[ordered]@{ <name> = <value>; [<name> = <value> ] ...}
```

<span data-ttu-id="c6dce-123">Атрибут [ordered] появился в PowerShell 3,0.</span><span class="sxs-lookup"><span data-stu-id="c6dce-123">The [ordered] attribute was introduced in PowerShell 3.0.</span></span>

### <a name="creating-hash-tables"></a><span data-ttu-id="c6dce-124">Создание хэш-таблиц</span><span class="sxs-lookup"><span data-stu-id="c6dce-124">Creating Hash Tables</span></span>

<span data-ttu-id="c6dce-125">Чтобы создать хэш-таблицу, следуйте приведенным ниже рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="c6dce-125">To create a hash table, follow these guidelines:</span></span>

- <span data-ttu-id="c6dce-126">Начните хэш-таблицу со знака @.</span><span class="sxs-lookup"><span data-stu-id="c6dce-126">Begin the hash table with an at sign (@).</span></span>
- <span data-ttu-id="c6dce-127">Заключите хэш-таблицу в фигурные скобки ( {} ).</span><span class="sxs-lookup"><span data-stu-id="c6dce-127">Enclose the hash table in braces ({}).</span></span>
- <span data-ttu-id="c6dce-128">Введите одну или несколько пар "ключ-значение" для содержимого хэш-таблицы.</span><span class="sxs-lookup"><span data-stu-id="c6dce-128">Enter one or more key/value pairs for the content of the hash table.</span></span>
- <span data-ttu-id="c6dce-129">Используйте знак равенства (=) для отделения каждого ключа от его значения.</span><span class="sxs-lookup"><span data-stu-id="c6dce-129">Use an equal sign (=) to separate each key from its value.</span></span>
- <span data-ttu-id="c6dce-130">Используйте точку с запятой (;) или разрыв строки для разделения пар «ключ-значение».</span><span class="sxs-lookup"><span data-stu-id="c6dce-130">Use a semicolon (;) or a line break to separate the key/value pairs.</span></span>
- <span data-ttu-id="c6dce-131">Ключ, содержащий пробелы, должен быть заключен в кавычки.</span><span class="sxs-lookup"><span data-stu-id="c6dce-131">Key that contains spaces must be enclosed in quotation marks.</span></span> <span data-ttu-id="c6dce-132">Значения должны быть допустимыми выражениями PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6dce-132">Values must be valid PowerShell expressions.</span></span> <span data-ttu-id="c6dce-133">Строки должны быть заключены в кавычки, даже если они не содержат пробелов.</span><span class="sxs-lookup"><span data-stu-id="c6dce-133">Strings must appear in quotation marks, even if they do not include spaces.</span></span>
- <span data-ttu-id="c6dce-134">Чтобы управлять хэш-таблицей, сохраните ее в переменной.</span><span class="sxs-lookup"><span data-stu-id="c6dce-134">To manage the hash table, save it in a variable.</span></span>
- <span data-ttu-id="c6dce-135">При назначении упорядоченной хэш-таблицы переменной поместите атрибут [ordered] перед символом "@".</span><span class="sxs-lookup"><span data-stu-id="c6dce-135">When assigning an ordered hash table to a variable, place the [ordered] attribute before the "@" symbol.</span></span> <span data-ttu-id="c6dce-136">Если поместить его перед именем переменной, команда завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c6dce-136">If you place it before the variable name, the command fails.</span></span>

<span data-ttu-id="c6dce-137">Чтобы создать пустую хэш-таблицу в значении $hash, введите:</span><span class="sxs-lookup"><span data-stu-id="c6dce-137">To create an empty hash table in the value of $hash, type:</span></span>

```powershell
$hash = @{}
```

<span data-ttu-id="c6dce-138">При создании хэш-таблицы можно также добавить в нее ключи и значения.</span><span class="sxs-lookup"><span data-stu-id="c6dce-138">You can also add keys and values to a hash table when you create it.</span></span> <span data-ttu-id="c6dce-139">Например, следующая инструкция создает хэш-таблицу с тремя ключами.</span><span class="sxs-lookup"><span data-stu-id="c6dce-139">For example, the following statement creates a hash table with three keys.</span></span>

```powershell
$hash = @{ Number = 1; Shape = "Square"; Color = "Blue"}
```

### <a name="creating-ordered-dictionaries"></a><span data-ttu-id="c6dce-140">Создание упорядоченных словарей</span><span class="sxs-lookup"><span data-stu-id="c6dce-140">Creating Ordered Dictionaries</span></span>

<span data-ttu-id="c6dce-141">Можно создать упорядоченный словарь, добавив объект типа Ордереддиктионари, но самый простой способ создать упорядоченный словарь — использовать атрибут [ordered].</span><span class="sxs-lookup"><span data-stu-id="c6dce-141">You can create an ordered dictionary by adding an object of the OrderedDictionary type, but the easiest way to create an ordered dictionary is use the [Ordered] attribute.</span></span>

<span data-ttu-id="c6dce-142">Атрибут [ordered] представлен в PowerShell 3,0.</span><span class="sxs-lookup"><span data-stu-id="c6dce-142">The [ordered] attribute is introduced in PowerShell 3.0.</span></span>

<span data-ttu-id="c6dce-143">Поместите атрибут непосредственно перед символом "@".</span><span class="sxs-lookup"><span data-stu-id="c6dce-143">Place the attribute immediately before the "@" symbol.</span></span>

```powershell
$hash = [ordered]@{ Number = 1; Shape = "Square"; Color = "Blue"}
```

<span data-ttu-id="c6dce-144">Упорядоченные словари можно использовать так же, как и хэш-таблицы.</span><span class="sxs-lookup"><span data-stu-id="c6dce-144">You can use ordered dictionaries in the same way that you use hash tables.</span></span>
<span data-ttu-id="c6dce-145">Любой из этих типов можно использовать в качестве значения параметров, которые принимают хэш-таблицу или словарь (iDictionary).</span><span class="sxs-lookup"><span data-stu-id="c6dce-145">Either type can be used as the value of parameters that take a hash table or dictionary (iDictionary).</span></span>

<span data-ttu-id="c6dce-146">Нельзя использовать атрибут [ordered] для преобразования или приведения хэш-таблицы.</span><span class="sxs-lookup"><span data-stu-id="c6dce-146">You cannot use the [ordered] attribute to convert or cast a hash table.</span></span> <span data-ttu-id="c6dce-147">Если поместить упорядоченный атрибут перед именем переменной, команда завершится со следующим сообщением об ошибке.</span><span class="sxs-lookup"><span data-stu-id="c6dce-147">If you place the ordered attribute before the variable name, the command fails with the following error message.</span></span>

```powershell
PS C:\> [ordered]$hash = @{}
At line:1 char:1
+ [ordered]$hash = @{}
+ [!INCLUDE[]()]
The ordered attribute can be specified only on a hash literal node.
+ CategoryInfo          : ParserError: (:) [], ParentContainsErrorRecordExc
eption
+ FullyQualifiedErrorId : OrderedAttributeOnlyOnHashLiteralNode
```

<span data-ttu-id="c6dce-148">Чтобы исправить выражение, переместите атрибут [ordered].</span><span class="sxs-lookup"><span data-stu-id="c6dce-148">To correct the expression, move the [ordered] attribute.</span></span>

```powershell
PS C:\> $hash = [ordered]@{}
```

<span data-ttu-id="c6dce-149">Можно привести упорядоченный словарь к хэш-таблице, но нельзя восстановить упорядоченный атрибут, даже если очистить переменную и ввести новые значения.</span><span class="sxs-lookup"><span data-stu-id="c6dce-149">You can cast an ordered dictionary to a hash table, but you cannot recover the ordered attribute, even if you clear the variable and enter new values.</span></span> <span data-ttu-id="c6dce-150">Для повторного создания заказа необходимо удалить и повторно создать переменную.</span><span class="sxs-lookup"><span data-stu-id="c6dce-150">To re-establish the order, you must remove and recreate the variable.</span></span>

```
PS C:\> [hashtable]$hash = [ordered]@{
>> Number = 1; Shape = "Square"; Color = "Blue"}
PS C:\> $hash

Name                           Value
----                           -----
Color                          Blue
Shape                          Square
Number                         1
```

### <a name="displaying-hash-tables"></a><span data-ttu-id="c6dce-151">Отображение хэш-таблиц</span><span class="sxs-lookup"><span data-stu-id="c6dce-151">Displaying Hash Tables</span></span>

<span data-ttu-id="c6dce-152">Чтобы отобразить хэш-таблицу, сохраненную в переменной, введите имя переменной.</span><span class="sxs-lookup"><span data-stu-id="c6dce-152">To display a hash table that is saved in a variable, type the variable name.</span></span>
<span data-ttu-id="c6dce-153">По умолчанию хэш-таблицы отображаются в виде таблицы с одним столбцом для ключей и одной для значений.</span><span class="sxs-lookup"><span data-stu-id="c6dce-153">By default, a hash tables is displayed as a table with one column for keys and one for values.</span></span>

```powershell
C:\PS> $hash

Name                           Value
----                           -----
Shape                          Square
Color                          Blue
Number                         1
```

<span data-ttu-id="c6dce-154">Хэш-таблицы имеют свойства "ключи" и "значения".</span><span class="sxs-lookup"><span data-stu-id="c6dce-154">Hash tables have Keys and Values properties.</span></span> <span data-ttu-id="c6dce-155">Используйте точечную нотацию для вывода всех ключей или всех значений.</span><span class="sxs-lookup"><span data-stu-id="c6dce-155">Use dot notation to display all of the keys or all of the values.</span></span>

```powershell
C:\PS> $hash.keys
Number
Shape
Color

C:\PS> $hash.values
1
Square
Blue
```

<span data-ttu-id="c6dce-156">Каждое имя ключа является также свойством хэш-таблицы, а его значением является значение свойства Key-Name.</span><span class="sxs-lookup"><span data-stu-id="c6dce-156">Each key name is also a property of the hash table, and its value is the value of the key-name property.</span></span> <span data-ttu-id="c6dce-157">Используйте следующий формат для вывода значений свойств.</span><span class="sxs-lookup"><span data-stu-id="c6dce-157">Use the following format to display the property values.</span></span>

```powershell
$hashtable.<key>
<value>
```

<span data-ttu-id="c6dce-158">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6dce-158">For example:</span></span>

```powershell
C:\PS> $hash.Number
1

C:\PS> $hash.Color
Blue
```

<span data-ttu-id="c6dce-159">Если имя ключа конфликтует с одним из имен свойств типа HashTable, можно использовать `PSBase` для доступа к этим свойствам.</span><span class="sxs-lookup"><span data-stu-id="c6dce-159">If the key name collides with one of the property names of the HashTable type, you can use `PSBase` to access those properties.</span></span> <span data-ttu-id="c6dce-160">Например, если имя ключа равно и необходимо `keys` вернуть коллекцию ключей, используйте следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="c6dce-160">For example, if the key name is `keys` and you want to return the collection of Keys, use this syntax:</span></span>

```powershell
$hashtable.PSBase.Keys
```

<span data-ttu-id="c6dce-161">Хэш-таблицы имеют свойство Count, которое указывает количество пар "ключ-значение" в хэш-таблице.</span><span class="sxs-lookup"><span data-stu-id="c6dce-161">Hash tables have a Count property that indicates the number of key-value pairs in the hash table.</span></span>

```powershell
C:\PS> $hash.count
3
```

<span data-ttu-id="c6dce-162">Таблицы хэш-таблиц не являются массивами, поэтому нельзя использовать целое число в качестве индекса в хэш-таблице, но можно использовать имя ключа для индексации в хэш-таблице.</span><span class="sxs-lookup"><span data-stu-id="c6dce-162">Hash table tables are not arrays, so you cannot use an integer as an index into the hash table, but you can use a key name to index into the hash table.</span></span>
<span data-ttu-id="c6dce-163">Если ключ является строковым значением, заключите имя ключа в кавычки.</span><span class="sxs-lookup"><span data-stu-id="c6dce-163">If the key is a string value, enclose the key name in quotation marks.</span></span>

<span data-ttu-id="c6dce-164">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6dce-164">For example:</span></span>

```powershell
C:\PS> $hash["Number"]
1
```

### <a name="adding-and-removing-keys-and-values"></a><span data-ttu-id="c6dce-165">Добавление и удаление ключей и значений</span><span class="sxs-lookup"><span data-stu-id="c6dce-165">Adding and Removing Keys and Values</span></span>

<span data-ttu-id="c6dce-166">Чтобы добавить ключи и значения в хэш-таблицу, используйте следующий формат команды:</span><span class="sxs-lookup"><span data-stu-id="c6dce-166">To add keys and values to a hash table, use the following command format.</span></span>

```powershell
$hash["<key>"] = "<value>"
```

<span data-ttu-id="c6dce-167">Например, чтобы добавить в хэш-таблицу ключ "Time" со значением "Now", используйте следующий формат инструкции.</span><span class="sxs-lookup"><span data-stu-id="c6dce-167">For example, to add a "Time" key with a value of "Now" to the hash table, use the following statement format.</span></span>

```powershell
$hash["Time"] = "Now"
```

<span data-ttu-id="c6dce-168">Также можно добавить ключи и значения в хэш-таблицу с помощью метода Add объекта System. Collections. Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c6dce-168">You can also add keys and values to a hash table by using the Add method of the System.Collections.Hashtable object.</span></span> <span data-ttu-id="c6dce-169">Метод Add имеет следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="c6dce-169">The Add method has the following syntax:</span></span>

```powershell
Add(Key, Value)
```

<span data-ttu-id="c6dce-170">Например, чтобы добавить в хэш-таблицу ключ "Time" со значением "Now", используйте следующий формат инструкции.</span><span class="sxs-lookup"><span data-stu-id="c6dce-170">For example, to add a "Time" key with a value of "Now" to the hash table, use the following statement format.</span></span>

```powershell
$hash.Add("Time", "Now")
```

<span data-ttu-id="c6dce-171">Кроме того, можно добавить ключи и значения в хэш-таблицу с помощью оператора сложения (+), чтобы добавить хэш-таблицу в существующую хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c6dce-171">And, you can add keys and values to a hash table by using the addition operator (+) to add a hash table to an existing hash table.</span></span> <span data-ttu-id="c6dce-172">Например, следующая инструкция добавляет ключ "Time" со значением "Now" в хэш-таблицу в переменной $hash.</span><span class="sxs-lookup"><span data-stu-id="c6dce-172">For example, the following statement adds a "Time" key with a value of "Now" to the hash table in the $hash variable.</span></span>

```powershell
$hash = $hash + @{Time="Now"}
```

<span data-ttu-id="c6dce-173">Можно также добавлять значения, хранящиеся в переменных.</span><span class="sxs-lookup"><span data-stu-id="c6dce-173">You can also add values that are stored in variables.</span></span>

```powershell
$t = "Today"
$now = (Get-Date)

$hash.Add($t, $now)
```

<span data-ttu-id="c6dce-174">Оператор вычитания нельзя использовать для удаления пары "ключ-значение" из хэш-таблицы, но можно использовать метод Remove объекта Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c6dce-174">You cannot use a subtraction operator to remove a key/value pair from a hash table, but you can use the Remove method of the Hashtable object.</span></span> <span data-ttu-id="c6dce-175">Метод Remove принимает ключ в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="c6dce-175">The Remove method takes the key as its value.</span></span>

<span data-ttu-id="c6dce-176">Метод Remove имеет следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="c6dce-176">The Remove method has the following syntax:</span></span>

```
Remove(Key)
```

<span data-ttu-id="c6dce-177">Например, чтобы удалить пару "время = теперь ключ — значение" из хэш-таблицы в значении переменной $hash, введите:</span><span class="sxs-lookup"><span data-stu-id="c6dce-177">For example, to remove the Time=Now key/value pair from the hash table in the value of the $hash variable, type:</span></span>

```powershell
$hash.Remove("Time")
```

<span data-ttu-id="c6dce-178">Вы можете использовать все свойства и методы объектов Hashtable в PowerShell, включая Contains, Clear, Clone и CopyTo.</span><span class="sxs-lookup"><span data-stu-id="c6dce-178">You can use all of the properties and methods of Hashtable objects in PowerShell, including Contains, Clear, Clone, and CopyTo.</span></span> <span data-ttu-id="c6dce-179">Дополнительные сведения об объектах Hashtable см. в разделе [System. Collections. Hashtable](/dotnet/api/system.collections.hashtable).</span><span class="sxs-lookup"><span data-stu-id="c6dce-179">For more information about Hashtable objects, see [System.Collections.Hashtable](/dotnet/api/system.collections.hashtable).</span></span>

### <a name="object-types-in-hashtables"></a><span data-ttu-id="c6dce-180">Типы объектов в хэш-таблицах</span><span class="sxs-lookup"><span data-stu-id="c6dce-180">Object Types in HashTables</span></span>

<span data-ttu-id="c6dce-181">Ключи и значения в хэш-таблице могут иметь любой тип объекта .NET, а одна хэш-таблица может иметь ключи и значения нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="c6dce-181">The keys and values in a hash table can have any .NET object type, and a single hash table can have keys and values of multiple types.</span></span>

<span data-ttu-id="c6dce-182">Следующая инструкция создает хэш-таблицу строк имени процесса и значения объекта Process и сохраняет их в `$p` переменной.</span><span class="sxs-lookup"><span data-stu-id="c6dce-182">The following statement creates a hash table of process name strings and process object values and saves it in the `$p` variable.</span></span>

```powershell
$p = @{"PowerShell" = (Get-Process PowerShell);
"Notepad" = (Get-Process notepad)}
```

<span data-ttu-id="c6dce-183">Можно отобразить хэш-таблицу в `$p` и использовать свойства Key-Name для вывода значений.</span><span class="sxs-lookup"><span data-stu-id="c6dce-183">You can display the hash table in `$p` and use the key-name properties to display the values.</span></span>

```powershell
C:\PS> $p

Name                           Value
----                           -----
PowerShell                     System.Diagnostics.Process (PowerShell)
Notepad                        System.Diagnostics.Process (notepad)

C:\PS> $p.PowerShell

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    441      24    54196      54012   571     5.10   1788 PowerShell

C:\PS> $p.keys | foreach {$p.$_.handles}
441
251
```

<span data-ttu-id="c6dce-184">Ключи в хэш-таблице могут также иметь любой тип .NET.</span><span class="sxs-lookup"><span data-stu-id="c6dce-184">The keys in a hash table can also be any .NET type.</span></span> <span data-ttu-id="c6dce-185">Следующая инструкция добавляет пару "ключ-значение" в хэш-таблицу в `$p` переменной.</span><span class="sxs-lookup"><span data-stu-id="c6dce-185">The following statement adds a key/value pair to the hash table in the `$p` variable.</span></span> <span data-ttu-id="c6dce-186">Ключ — это объект службы, представляющий службу WinRM, а значение — Текущее состояние службы.</span><span class="sxs-lookup"><span data-stu-id="c6dce-186">The key is a Service object that represents the WinRM service, and the value is the current status of the service.</span></span>

```powershell
C:\PS> $p = $p + @{(Get-Service WinRM) = ((Get-Service WinRM).Status)}
```

<span data-ttu-id="c6dce-187">Вы можете отобразить новую пару "ключ-значение" и получить к ней доступ с помощью тех же методов, которые используются для других пар в хэш-таблице.</span><span class="sxs-lookup"><span data-stu-id="c6dce-187">You can display and access the new key/value pair by using the same methods that you use for other pairs in the hash table.</span></span>

```powershell
C:\PS> $p

Name                           Value
----                           -----
PowerShell                     System.Diagnostics.Process (PowerShell)
Notepad                        System.Diagnostics.Process (notepad)
System.ServiceProcess.Servi... Running

C:\PS> $p.keys
PowerShell
Notepad

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...

C:\PS> $p.keys | foreach {$_.name}
winrm
```

<span data-ttu-id="c6dce-188">Ключи и значения в хэш-таблице также могут быть объектами Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c6dce-188">The keys and values in a hash table can also be Hashtable objects.</span></span> <span data-ttu-id="c6dce-189">Следующая инструкция добавляет пару "ключ-значение" в хэш-таблицу в `$p` переменной, в которой ключ является строкой, Hash2, а значение — хэш-таблицей с тремя парами "ключ-значение".</span><span class="sxs-lookup"><span data-stu-id="c6dce-189">The following statement adds key/value pair to the hash table in the `$p` variable in which the key is a string, Hash2, and the value is a hash table with three key/value pairs.</span></span>

```powershell
C:\PS> $p = $p + @{"Hash2"= @{a=1; b=2; c=3}}
```

<span data-ttu-id="c6dce-190">Вы можете отображать новые значения и получать к ним доступ с помощью тех же методов.</span><span class="sxs-lookup"><span data-stu-id="c6dce-190">You can display and access the new values by using the same methods.</span></span>

```powershell
C:\PS> $p

Name                           Value
----                           -----
PowerShell                     System.Diagnostics.Process (PowerShell)
Notepad                        System.Diagnostics.Process (notepad)
System.ServiceProcess.Servi... Running
Hash2                          {a, b, c}

C:\PS> $p.Hash2

Name                           Value
----                           -----
a                              1
b                              2
c                              3

C:\PS> $p.Hash2.b
2
```

### <a name="sorting-keys-and-values"></a><span data-ttu-id="c6dce-191">Сортировка ключей и значений</span><span class="sxs-lookup"><span data-stu-id="c6dce-191">Sorting Keys and Values</span></span>

<span data-ttu-id="c6dce-192">Элементы в хэш-таблице неупорядочены по отдельности.</span><span class="sxs-lookup"><span data-stu-id="c6dce-192">The items in a hash table are intrinsically unordered.</span></span> <span data-ttu-id="c6dce-193">Пары "ключ-значение" могут отображаться в отдельном порядке при каждом их отображении.</span><span class="sxs-lookup"><span data-stu-id="c6dce-193">The key/value pairs might appear in a different order each time that you display them.</span></span>

<span data-ttu-id="c6dce-194">Хотя хэш-таблицу нельзя отсортировать, можно использовать метод GetEnumerator хэш-таблиц для перечисления ключей и значений, а затем использовать командлет Sort-Object для сортировки перечисленных значений для вывода.</span><span class="sxs-lookup"><span data-stu-id="c6dce-194">Although you cannot sort a hash table, you can use the GetEnumerator method of hash tables to enumerate the keys and values, and then use the Sort-Object cmdlet to sort the enumerated values for display.</span></span>

<span data-ttu-id="c6dce-195">Например, следующие команды перечисляют ключи и значения в хэш-таблице в `$p` переменной, а затем сортируют эти ключи в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="c6dce-195">For example, the following commands enumerate the keys and values in the hash table in the `$p` variable and then sort the keys in alphabetical order.</span></span>

```powershell
C:\PS> $p.GetEnumerator() | Sort-Object -Property key

Name                           Value
----                           -----
Notepad                        System.Diagnostics.Process (notepad)
PowerShell                     System.Diagnostics.Process (PowerShell)
System.ServiceProcess.Servi... Running
```

<span data-ttu-id="c6dce-196">Следующая команда использует ту же процедуру для сортировки хэш-значений в порядке убывания.</span><span class="sxs-lookup"><span data-stu-id="c6dce-196">The following command uses the same procedure to sort the hash values in descending order.</span></span>

```powershell
C:\PS> $p.getenumerator() | Sort-Object -Property Value -Descending

Name                           Value
----                           -----
PowerShell                     System.Diagnostics.Process (PowerShell)
Notepad                        System.Diagnostics.Process (notepad)
System.ServiceProcess.Servi... Running
```

### <a name="creating-objects-from-hash-tables"></a><span data-ttu-id="c6dce-197">Создание объектов из хэш-таблиц</span><span class="sxs-lookup"><span data-stu-id="c6dce-197">Creating Objects from Hash Tables</span></span>

<span data-ttu-id="c6dce-198">Начиная с PowerShell 3,0, можно создать объект из хэш-таблицы свойств и значений свойств.</span><span class="sxs-lookup"><span data-stu-id="c6dce-198">Beginning in PowerShell 3.0, you can create an object from a hash table of properties and property values.</span></span>

<span data-ttu-id="c6dce-199">Синтаксис выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6dce-199">The syntax is as follows:</span></span>

```powershell
[<class-name>]@{
  <property-name>=<property-value>
  <property-name>=<property-value>
}
```

<span data-ttu-id="c6dce-200">Этот метод работает только для классов, имеющих конструктор со значением NULL, то есть конструктор, не имеющий параметров.</span><span class="sxs-lookup"><span data-stu-id="c6dce-200">This method works only for classes that have a null constructor, that is, a constructor that has no parameters.</span></span> <span data-ttu-id="c6dce-201">Свойства объекта должны быть общедоступными и настраиваемыми.</span><span class="sxs-lookup"><span data-stu-id="c6dce-201">The object properties must be public and settable.</span></span>

<span data-ttu-id="c6dce-202">Дополнительные сведения см. в разделе [about_Object_Creation](about_Object_Creation.md).</span><span class="sxs-lookup"><span data-stu-id="c6dce-202">For more information, see [about_Object_Creation](about_Object_Creation.md).</span></span>

### <a name="convertfrom-stringdata"></a><span data-ttu-id="c6dce-203">ConvertFrom-StringData</span><span class="sxs-lookup"><span data-stu-id="c6dce-203">ConvertFrom-StringData</span></span>

<span data-ttu-id="c6dce-204">`ConvertFrom-StringData`Командлет преобразует строку или строку в паре "ключ-значение" в хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c6dce-204">The `ConvertFrom-StringData` cmdlet converts a string or a here-string of key/value pairs into a hash table.</span></span> <span data-ttu-id="c6dce-205">Командлет можно безопасно использовать `ConvertFrom-StringData` в разделе данных скрипта. его можно использовать с `Import-LocalizedData` командлетом для вывода сообщений пользователя в языке и региональных параметрах пользовательского интерфейса текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="c6dce-205">You can use the `ConvertFrom-StringData` cmdlet safely in the Data section of a script, and you can use it with the `Import-LocalizedData` cmdlet to display user messages in the user-interface (UI) culture of the current user.</span></span>

<span data-ttu-id="c6dce-206">Здесь строки особенно полезны, если значения в хэш-таблице содержат кавычки.</span><span class="sxs-lookup"><span data-stu-id="c6dce-206">Here-strings are especially useful when the values in the hash table include quotation marks.</span></span> <span data-ttu-id="c6dce-207">Дополнительные сведения о строках см. в разделе [about_Quoting_Rules](about_Quoting_Rules.md).</span><span class="sxs-lookup"><span data-stu-id="c6dce-207">For more information about here-strings, see [about_Quoting_Rules](about_Quoting_Rules.md).</span></span>

<span data-ttu-id="c6dce-208">В следующем примере показано, как создать строку с сообщениями пользователя в предыдущем примере и как использовать `ConvertFrom-StringData` для преобразования их из строки в хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c6dce-208">The following example shows how to create a here-string of the user messages in the previous example and how to use `ConvertFrom-StringData` to convert them from a string into a hash table.</span></span>

<span data-ttu-id="c6dce-209">Следующая команда создает строку "ключ-значение", а затем сохраняет ее в \$ строковой переменной.</span><span class="sxs-lookup"><span data-stu-id="c6dce-209">The following command creates a here-string of the key/value pairs and then saves it in the \$string variable.</span></span>

```powershell
C:\PS> $string = @"
Msg1 = Type "Windows".
Msg2 = She said, "Hello, World."
Msg3 = Enter an alias (or "nickname").
"@
```

<span data-ttu-id="c6dce-210">Эта команда использует командлет ConvertFrom-StringData для преобразования строки Here в хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c6dce-210">This command uses the ConvertFrom-StringData cmdlet to convert the here-string into a hash table.</span></span>

```powershell
C:\PS> ConvertFrom-StringData $string

Name                           Value
----                           -----
Msg3                           Enter an alias (or "nickname").
Msg2                           She said, "Hello, World."
Msg1                           Type "Windows".
```

<span data-ttu-id="c6dce-211">Дополнительные сведения о строках см. в разделе [about_Quoting_Rules](about_Quoting_Rules.md).</span><span class="sxs-lookup"><span data-stu-id="c6dce-211">For more information about here-strings, see [about_Quoting_Rules](about_Quoting_Rules.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c6dce-212">СМ. ТАКЖЕ</span><span class="sxs-lookup"><span data-stu-id="c6dce-212">SEE ALSO</span></span>

[<span data-ttu-id="c6dce-213">about_Arrays</span><span class="sxs-lookup"><span data-stu-id="c6dce-213">about_Arrays</span></span>](about_Arrays.md)

[<span data-ttu-id="c6dce-214">about_Object_Creation</span><span class="sxs-lookup"><span data-stu-id="c6dce-214">about_Object_Creation</span></span>](about_Object_Creation.md)

[<span data-ttu-id="c6dce-215">about_Quoting_Rules</span><span class="sxs-lookup"><span data-stu-id="c6dce-215">about_Quoting_Rules</span></span>](about_Quoting_Rules.md)

[<span data-ttu-id="c6dce-216">about_Script_Internationalization</span><span class="sxs-lookup"><span data-stu-id="c6dce-216">about_Script_Internationalization</span></span>](about_Script_Internationalization.md)

[<span data-ttu-id="c6dce-217">ConvertFrom-StringData</span><span class="sxs-lookup"><span data-stu-id="c6dce-217">ConvertFrom-StringData</span></span>](xref:Microsoft.PowerShell.Utility.ConvertFrom-StringData)

[<span data-ttu-id="c6dce-218">Import-LocalizedData</span><span class="sxs-lookup"><span data-stu-id="c6dce-218">Import-LocalizedData</span></span>](xref:Microsoft.PowerShell.Utility.Import-LocalizedData)

[<span data-ttu-id="c6dce-219">System.Collections.Hashtable</span><span class="sxs-lookup"><span data-stu-id="c6dce-219">System.Collections.Hashtable</span></span>](/dotnet/api/system.collections.hashtable)