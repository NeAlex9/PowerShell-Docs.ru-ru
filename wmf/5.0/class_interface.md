---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 116f79a95126d0a1c579a95ec99eb5d8b75cc1e0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
---
# <a name="declare-implemented-interface"></a><span data-ttu-id="34908-102">Объявление реализованного интерфейса</span><span class="sxs-lookup"><span data-stu-id="34908-102">Declare Implemented Interface</span></span>

<span data-ttu-id="34908-103">Реализованные интерфейсы можно объявить после базовых типов или сразу после двоеточия (:), если базовый тип не указан.</span><span class="sxs-lookup"><span data-stu-id="34908-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="34908-104">Все имена типов следует разделять запятыми.</span><span class="sxs-lookup"><span data-stu-id="34908-104">Separate all type names by using commas.</span></span> <span data-ttu-id="34908-105">Это очень похоже на синтаксис C#.</span><span class="sxs-lookup"><span data-stu-id="34908-105">It’s very similar to C# syntax.</span></span>

```powershell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```
