---
ms.date: 09/13/2016
ms.topic: reference
title: Расширение объектов выходных данных
description: Расширение объектов выходных данных
ms.openlocfilehash: 9fea476e3032002bd206609313581cc6373dfddc
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92652901"
---
# <a name="extending-output-objects"></a>Расширение объектов выходных данных

.NET Framework объекты, возвращаемые командлетами, функциями и скриптами, можно расширить с помощью файлов типов (. ps1xml). Файлы типов — это файлы на основе XML, которые позволяют добавлять свойства и методы в существующие объекты. Например, Windows PowerShell предоставляет Types.ps1XML-файл, который добавляет элементы в несколько существующих объектов .NET Framework. Types.ps1XML-файл находится в каталоге установки Windows PowerShell ( `$pshome` ). Вы можете создать собственный файл типов, чтобы расширить эти объекты или расширить другие объекты. При расширении объекта с помощью файла типов любой экземпляр объекта расширяется с помощью новых элементов.

## <a name="extending-the-systemarray-object"></a>Расширение объекта System. Array

В следующем примере показано, как Windows PowerShell расширяет объект [System. Array](/dotnet/api/System.Array) в Types.ps1XML-файле. По умолчанию объекты [System. Array](/dotnet/api/System.Array) имеют `Length` свойство, которое перечисляет количество объектов в массиве. Однако, поскольку имя "Length" явно не описывает свойство, Windows PowerShell добавляет `Count` свойство Alias, которое отображает то же значение, что и `Length` свойство. Следующий XML-код добавляет `Count` свойство в тип [System. Array](/dotnet/api/System.Array) .

```xml
<Type>
  <Name>System.Array</Name>
  <Members>
    <AliasProperty>
      <Name>Count</Name>
      <ReferencedMemberName>Length</ReferencedMemberName>
    </AliasProperty>
  </Members>
</Type>

```

Чтобы просмотреть это новое свойство псевдонима, используйте команду [Get-Member](/powershell/module/Microsoft.PowerShell.Utility/Get-Member) для любого массива, как показано в следующем примере.

```powershell
Get-Member -InputObject (1,2,3,4)
```

Команда возвращает следующие результаты.

```output
Name           MemberType    Definition
----           ----------    ----------
Count          AliasProperty Count = Length
Address        Method        System.Object& Address(Int32 )
Clone          Method        System.Object Clone()
CopyTo         Method        System.Void CopyTo(Array array, Int32 index):
Equals         Method        System.Boolean Equals(Object obj)
Get            Method        System.Object Get(Int32 )
...
Length         Property      System.Int32 Length {get;}
```

`Count` `Length` Для определения количества объектов в массиве можно использовать свойство или свойство. Пример:

```powershell
PS> (1, 2, 3, 4).Count
```

```output
4
```

```powershell
PS> (1, 2, 3, 4).Length
```

```output
4
```

## <a name="custom-types-files"></a>Файлы пользовательских типов

Чтобы создать файл пользовательских типов, начните с копирования существующего файла типов. Новый файл может иметь любое имя, но его имя должно иметь расширение ps1xml. При копировании файла можно поместить новый файл в любой каталог, доступный для Windows PowerShell, но это полезно для размещения файлов в каталоге установки Windows PowerShell ( `$pshome` ) или в подкаталоге каталога установки.

Чтобы добавить в файл собственные расширенные типы, добавьте элемент Types для каждого объекта, который требуется расширить. В следующих разделах приведены примеры.

- Дополнительные сведения о добавлении свойств и наборов свойств см. в разделе [Расширенные свойства](./extending-properties-for-objects.md) .

- Дополнительные сведения о добавлении методов см. в разделе [Расширенные методы](./defining-default-methods-for-objects.md).

- Дополнительные сведения о добавлении наборов элементов см. в разделе [расширенные наборы элементов](./defining-default-member-sets-for-objects.md).

После определения собственных расширенных типов используйте один из следующих методов, чтобы сделать доступными расширенные объекты:

- Чтобы сделать файл расширенных типов доступным для текущего сеанса, используйте командлет [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) , чтобы добавить новый файл. Если требуется, чтобы типы применялись к типам, определенным в файлах других типов (включая файл Types.ps1XML), используйте `PrependData` параметр командлета [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) .
- Чтобы сделать файл расширенных типов доступным для всех будущих сеансов, добавьте файл типов в модуль, экспортируйте текущий сеанс или добавьте команду [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) в профиль Windows PowerShell.

## <a name="signing-types-files"></a>Файлы типов подписывания

Файлы типов должны иметь цифровую подпись, чтобы предотвратить незаконное изменение, так как XML может включать блоки сценариев. Дополнительные сведения о добавлении цифровых подписей см. в разделе [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing)

## <a name="see-also"></a>См. также:

[Определение свойств по умолчанию для объектов](./extending-properties-for-objects.md)

[Определение методов по умолчанию для объектов](./defining-default-methods-for-objects.md)

[Определение наборов элементов по умолчанию для объектов](./defining-default-member-sets-for-objects.md)

[Запись командлета Windows PowerShell](./writing-a-windows-powershell-cmdlet.md)
