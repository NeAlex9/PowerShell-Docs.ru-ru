---
title: Элемент Кустомконтролнаме для ExpressionBinding для ошибка customcontrol для представления (Format) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ea821e8b-4d65-4263-b7e4-6aeca9f534c2
caps.latest.revision: 9
ms.openlocfilehash: b44ced75bbaac7c0744f347bdc97f87365b8fe39
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364113"
---
# <a name="customcontrolname-element-for-expressionbinding-for-customcontrol-for-view-format"></a><span data-ttu-id="4722b-102">Элемент CustomControlName для элемента ExpressionBinding для элемента CustomControl для элемента View (формат)</span><span class="sxs-lookup"><span data-stu-id="4722b-102">CustomControlName Element for ExpressionBinding for CustomControl for View (Format)</span></span>

<span data-ttu-id="4722b-103">Указывает имя общего элемента управления или элемента управления представления.</span><span class="sxs-lookup"><span data-stu-id="4722b-103">Specifies the name of a common control or a view control.</span></span> <span data-ttu-id="4722b-104">Этот элемент используется при определении пользовательского представления элемента управления.</span><span class="sxs-lookup"><span data-stu-id="4722b-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="4722b-105">Элемент конфигурации (Format) Виевдефинитионс элемент (Format) представление элемента Ошибка customcontrol для элемента представления (Format) Кустоментриес для ошибка customcontrol для элемента представления (Format) Кустоментри для Кустоментриес для представления (Format) Кустомитем Элемент для Кустоментри для элемента ExpressionBinding представления (Format) для элемента Кустомитем (Format) Кустомконтролнаме для привязки выражения Кустомитем (Format)</span><span class="sxs-lookup"><span data-stu-id="4722b-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format) ExpressionBinding Element for CustomItem (Format) CustomControlName Element for Expression Binding for CustomItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="4722b-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4722b-106">Syntax</span></span>

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="4722b-107">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="4722b-107">Attributes and Elements</span></span>

<span data-ttu-id="4722b-108">В следующих разделах описываются атрибуты, дочерние элементы и родительский элемент элемента `CustomControlName`.</span><span class="sxs-lookup"><span data-stu-id="4722b-108">The following sections describe attributes, child elements, and the parent element of the `CustomControlName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="4722b-109">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="4722b-109">Attributes</span></span>

<span data-ttu-id="4722b-110">Нет.</span><span class="sxs-lookup"><span data-stu-id="4722b-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="4722b-111">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="4722b-111">Child Elements</span></span>

<span data-ttu-id="4722b-112">Нет.</span><span class="sxs-lookup"><span data-stu-id="4722b-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="4722b-113">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="4722b-113">Parent Elements</span></span>

|<span data-ttu-id="4722b-114">Элемент</span><span class="sxs-lookup"><span data-stu-id="4722b-114">Element</span></span>|<span data-ttu-id="4722b-115">Описание</span><span class="sxs-lookup"><span data-stu-id="4722b-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="4722b-116">Элемент ExpressionBinding для Кустомитем (Format)</span><span class="sxs-lookup"><span data-stu-id="4722b-116">ExpressionBinding Element for CustomItem (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="4722b-117">Определяет данные, отображаемые элементом управления.</span><span class="sxs-lookup"><span data-stu-id="4722b-117">Defines the data that is displayed by the control.</span></span>|

## <a name="text-value"></a><span data-ttu-id="4722b-118">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="4722b-118">Text Value</span></span>

<span data-ttu-id="4722b-119">Укажите имя элемента управления.</span><span class="sxs-lookup"><span data-stu-id="4722b-119">Specify the name of the control.</span></span>

## <a name="remarks"></a><span data-ttu-id="4722b-120">Замечания</span><span class="sxs-lookup"><span data-stu-id="4722b-120">Remarks</span></span>

<span data-ttu-id="4722b-121">Можно создавать стандартные элементы управления, которые могут использоваться всеми представлениями файла форматирования, а также создавать элементы управления представления, которые могут использоваться в определенном представлении.</span><span class="sxs-lookup"><span data-stu-id="4722b-121">You can create common controls that can be used by all the views of a formatting file and you can create view controls that can be used by a specific view.</span></span> <span data-ttu-id="4722b-122">Имена этих элементов управления задаются следующими элементами.</span><span class="sxs-lookup"><span data-stu-id="4722b-122">The names of these controls are specified by the following elements.</span></span>

- [<span data-ttu-id="4722b-123">Элемент Name для элемента управления для элементов управления Configuration (Format)</span><span class="sxs-lookup"><span data-stu-id="4722b-123">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

- [<span data-ttu-id="4722b-124">Элемент Name для элемента управления для элементов управления в представлении (формат)</span><span class="sxs-lookup"><span data-stu-id="4722b-124">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a><span data-ttu-id="4722b-125">См. также:</span><span class="sxs-lookup"><span data-stu-id="4722b-125">See Also</span></span>

[<span data-ttu-id="4722b-126">Элемент Name для элемента управления для элементов управления Configuration (Format)</span><span class="sxs-lookup"><span data-stu-id="4722b-126">Name Element for Control for Controls for Configuration (Format)</span></span>](./name-element-for-control-for-controls-for-configuration-format.md)

[<span data-ttu-id="4722b-127">Элемент Name для элемента управления для элементов управления в представлении (формат)</span><span class="sxs-lookup"><span data-stu-id="4722b-127">Name Element for Control for Controls for View (Format)</span></span>](./name-element-for-control-for-controls-for-view-format.md)

[<span data-ttu-id="4722b-128">Элемент ExpressionBinding для Кустомитем (Format)</span><span class="sxs-lookup"><span data-stu-id="4722b-128">ExpressionBinding Element for CustomItem (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="4722b-129">Написание файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="4722b-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)