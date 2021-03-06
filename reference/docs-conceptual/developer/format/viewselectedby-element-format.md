---
ms.date: 09/13/2016
ms.topic: reference
title: Элемент ViewSelectedBy (формат)
description: Элемент ViewSelectedBy (формат)
ms.openlocfilehash: ac3c7de299b3009a067a476a024c6a6fcb5dce02
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92667714"
---
# <a name="viewselectedby-element-format"></a>Элемент ViewSelectedBy (формат)

Определяет объекты .NET, отображаемые представлением. Каждое представление должно содержать по крайней мере один объект .NET.

Элемент Виевдефинитионс (Format) View элемент (Format) Виевселектедби (формат)

## <a name="syntax"></a>Синтаксис

```xml
<ViewSelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
</ViewSelectedBy>
```

## <a name="attributes-and-elements"></a>Атрибуты и элементы

В следующих разделах описываются атрибуты, дочерние элементы и родительский элемент `ViewSelectedBy` элемента. Этот элемент должен содержать по крайней мере один `TypeName` или `SelectionSetName` дочерний элемент. Количество дочерних элементов, которые можно указать, не ограничено, а их порядок не является значимым.

### <a name="attributes"></a>Атрибуты

Отсутствует.

### <a name="child-elements"></a>Дочерние элементы

|Элемент|Описание|
|-------------|-----------------|
|[Элемент TypeName для элемента ViewSelectedBy (формат)](./typename-element-for-viewselectedby-format.md)|Необязательный элемент.<br /><br /> Задает объект .NET, отображаемый представлением.|
|[Элемент SelectionSetName для элемента ViewSelectedBy (формат)](./selectionsetname-element-for-viewselectedby-format.md)|Необязательный элемент.<br /><br /> Задает набор объектов .NET, отображаемых представлением.|

### <a name="parent-elements"></a>Родительские элементы

|Элемент|Описание|
|-------------|-----------------|
|[Элемент View (формат)](./view-element-format.md)|Определяет представление, в котором отображается один или несколько объектов .NET.|

## <a name="remarks"></a>Комментарии

Дополнительные сведения об использовании этого элемента в различных представлениях см. в разделе [компоненты табличного](./creating-a-table-view.md)представления, [Компоненты представления списка](./creating-a-list-view.md), [компоненты расширенного представления](./creating-a-wide-view.md)и [компоненты пользовательского элемента управления](./creating-custom-controls.md).

`SelectionSetName`Элемент используется, когда файл форматирования определяет набор объектов, отображаемых несколькими представлениями. Дополнительные сведения о том, как определяются и указываются наборы выбора, см. в разделе [Определение наборов объектов](./defining-selection-sets.md).

## <a name="example"></a>Пример

В следующем примере показано, как указать объект [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) для представления списка. Одна и та же схема используется для таблиц, расширенных и пользовательских представлений.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a>См. также:

[Создание представления списка](./creating-a-list-view.md)

[Создание представления таблицы](./creating-a-table-view.md)

[Создание широкого представления](./creating-a-wide-view.md)

[Создание пользовательских элементов управления](./creating-custom-controls.md)

[Определение наборов выделенных фрагментов](./defining-selection-sets.md)

[Элемент SelectionSetName для элемента ViewSelectedBy (формат)](./selectionsetname-element-for-viewselectedby-format.md)

[Элемент TypeName (Format)](./typename-element-for-viewselectedby-format.md)

[Написание файла форматирования PowerShell](./writing-a-powershell-formatting-file.md)
