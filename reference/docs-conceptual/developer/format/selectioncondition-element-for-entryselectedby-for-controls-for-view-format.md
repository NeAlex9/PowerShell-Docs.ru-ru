---
ms.date: 09/13/2016
ms.topic: reference
title: Элемент SelectionCondition для элемента EntrySelectedBy для элемента Controls для элемента View (формат)
description: Элемент SelectionCondition для элемента EntrySelectedBy для элемента Controls для элемента View (формат)
ms.openlocfilehash: 16b048e73195b3d6168724714ff223851dc1b20b
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92664853"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-view-format"></a>Элемент SelectionCondition для элемента EntrySelectedBy для элемента Controls для элемента View (формат)

Определяет условие, которое должно существовать для использования определения элемента управления. Этот элемент используется при определении элементов управления, которые могут использоваться представлением.

Элемент Configuration (Format) Виевдефинитионс элемент (формат) элемент представления (Format) управляет управляющий элемент (Format) элемент управления для элементов управления представления (Format) ошибка customcontrol для элементов управления элемента Кустоментриес представления (Format) для ошибка customcontrol для элементов управления для элемента Кустоментри представления (Format) Кустоментриес для элементов управления для представления (Format) Ентриселектедби элемента для Кустоментри для элементов управления для представления (Format) SelectionCondition в EntrySelectedBy для элементов управления представления (формат)

## <a name="syntax"></a>Синтаксис

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a>Атрибуты и элементы

В следующих разделах описываются атрибуты, дочерние элементы и родительский элемент `SelectionCondition` элемента.

### <a name="attributes"></a>Атрибуты

Отсутствует.

### <a name="child-elements"></a>Дочерние элементы

|Элемент|Описание|
|-------------|-----------------|
|[Элемент PropertyName для элемента SelectionCondition для элемента Controls для элемента View (формат)](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)|Необязательный элемент.<br /><br /> Указывает свойство .NET, которое запускает условие.|
|[Элемент ScriptBlock для элемента SelectionCondition для элемента Controls для элемента View (формат)](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)|Необязательный элемент.<br /><br /> Указывает скрипт, который запускает условие.|
|[Элемент SelectionSetName для элемента SelectionCondition для элемента Controls для элемента View (формат)](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)|Необязательный элемент.<br /><br /> Указывает набор типов .NET, которые инициируют условие.|
|[Элемент TypeName для элемента SelectionCondition для элемента Controls для элемента View (формат)](./typename-element-for-selectioncondition-for-controls-for-view-format.md)|Необязательный элемент.<br /><br /> Указывает тип .NET, который запускает условие.|

### <a name="parent-elements"></a>Родительские элементы

|Элемент|Описание|
|-------------|-----------------|
|[Элемент EntrySelectedBy для элемента CustomEntry для элемента Controls для элемента View (формат)](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|Определяет типы .NET, которые используют это определение элемента управления или условие, которое должно существовать, чтобы использовать это определение.|

## <a name="remarks"></a>Комментарии

При определении условия выбора применяются следующие требования.

- Условие выбора должно указывать по крайней мере одно имя свойства или блок скрипта, но не может указывать и то и другое.

- Условие выбора может указывать любое количество типов .NET или наборов выбора, но не может одновременно указывать оба типа.

Дополнительные сведения об использовании условий выбора см. в разделе [Определение условий для отображения данных](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>См. также:

[Элемент PropertyName для элемента SelectionCondition для элемента Controls для элемента View (формат)](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)

[Элемент ScriptBlock для элемента SelectionCondition для элемента Controls для элемента View (формат)](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)

[Элемент SelectionSetName для элемента SelectionCondition для элемента Controls для элемента View (формат)](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

[Элемент TypeName для элемента SelectionCondition для элемента Controls для элемента View (формат)](./typename-element-for-selectioncondition-for-controls-for-view-format.md)

[Элемент EntrySelectedBy для элемента CustomEntry для элемента Controls для элемента View (формат)](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)

[Написание файла форматирования PowerShell](./writing-a-powershell-formatting-file.md)
