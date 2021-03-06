---
ms.date: 07/09/2020
ms.topic: reference
title: Члены класса системы расширенного типа
description: Члены класса системы расширенного типа
ms.openlocfilehash: 06488ce423f363a285ab53b21ab45989654346dc
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92666847"
---
# <a name="extended-type-system-class-members"></a>Члены класса системы расширенного типа

ETS ссылается на ряд различных видов членов, типы которых определяются перечислением **псмембертипес** . К этим типам членов относятся свойства, методы, члены и наборы элементов, определяемые их собственным типом CLR. Например, **NoteProperty** определяется собственным типом **пснотепроперти** . Эти отдельные типы CLR имеют свои собственные уникальные свойства и общие свойства, унаследованные от [класса псмемберинфо](/dotnet/api/system.management.automation.psmemberinfo).

## <a name="the-psmemberinfo-class"></a>Класс Псмемберинфо

Класс **псмемберинфо** выступает в качестве базового класса для всех типов элементов ETS. Этот класс предоставляет следующие базовые свойства для всех типов CLR элементов.

- **Имя** свойство: имя элемента. Это имя может быть определено базовым объектом или определено с помощью PowerShell, когда предоставляются адаптированные члены или расширенные члены.
- Свойство **value** — значение, возвращенное из конкретного элемента. Каждый тип элемента определяет, как он обрабатывает его значение элемента.
- Свойство **типенамеофвалуе** : это имя типа CLR значения, возвращаемого свойством Value.

## <a name="accessing-members"></a>Доступ к членам

Доступ к коллекциям элементов можно получить с помощью свойств **Members**, **Methods** и **Properties** объекта **PSObject** .

## <a name="ets-properties"></a>Свойства ETS

Свойства ETS — это члены, которые можно рассматривать как свойства. По сути, они могут присутствовать в левой части выражения. К ним относятся свойства псевдонима, свойства кода, свойства PowerShell, свойства примечаний и свойства скриптов. Дополнительные сведения об этих типах свойств см. в разделе [Свойства ETS](properties.md).

## <a name="ets-methods"></a>Методы ETS

Методы ETS — это члены, которые могут принимать аргументы, могут возвращать результаты и не могут отображаться в левой части выражения. К ним относятся методы кода, методы PowerShell и методы скриптов.
Дополнительные сведения об этих типах методов см. в разделе [методы ETS](methods.md).
