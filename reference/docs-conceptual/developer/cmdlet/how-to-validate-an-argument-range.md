---
title: Проверка диапазона аргументов | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateRange attribute, example
ms.assetid: 3cba3ab7-c3b6-4d17-aa17-88377496551b
caps.latest.revision: 9
ms.openlocfilehash: a39e34d1f1c333185f09b4a934819e1368d29a48
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72365523"
---
# <a name="how-to-validate-an-argument-range"></a><span data-ttu-id="0f87b-102">Как проверить диапазон аргумента</span><span class="sxs-lookup"><span data-stu-id="0f87b-102">How to Validate an Argument Range</span></span>

<span data-ttu-id="0f87b-103">В этом примере показано, как указать правило проверки, которое среда выполнения Windows PowerShell может использовать для проверки минимального и максимального значений аргумента параметра перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="0f87b-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the minimum and maximum values of the parameter argument before the cmdlet is run.</span></span> <span data-ttu-id="0f87b-104">Это правило проверки задается путем объявления атрибута Валидатеранже.</span><span class="sxs-lookup"><span data-stu-id="0f87b-104">You set this validation rule by declaring the ValidateRange attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="0f87b-105">Дополнительные сведения о классе, который определяет этот атрибут, см. в разделе [System. Management. Automation. валидатеранжеаттрибуте](/dotnet/api/System.Management.Automation.ValidateRangeAttribute).</span><span class="sxs-lookup"><span data-stu-id="0f87b-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validaterangeattribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute).</span></span>

### <a name="to-validate-an-argument-range"></a><span data-ttu-id="0f87b-106">Проверка диапазона аргументов</span><span class="sxs-lookup"><span data-stu-id="0f87b-106">To validate an argument range</span></span>

- <span data-ttu-id="0f87b-107">Добавьте атрибут Валидатеранже, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="0f87b-107">Add the ValidateRange attribute as shown in the following code.</span></span> <span data-ttu-id="0f87b-108">В этом примере указывается диапазон от 0 до 5 для параметра `InputData`.</span><span class="sxs-lookup"><span data-stu-id="0f87b-108">This example specifies a range of 0 to 5 for the `InputData` parameter.</span></span>

    ```csharp
    [ValidateRange(0, 5)]
    [Parameter(Position = 0, Mandatory = true)]
    public int InputData
    {
      get { return inputData; }
      set { inputData = value; }
    }
    private int inputData;
    ```

<span data-ttu-id="0f87b-109">Дополнительные сведения об объявлении этого атрибута см. в разделе [объявление атрибута валидатеранже](./validaterange-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="0f87b-109">For more information about how to declare this attribute, see [ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0f87b-110">См. также:</span><span class="sxs-lookup"><span data-stu-id="0f87b-110">See Also</span></span>

[<span data-ttu-id="0f87b-111">Объявление атрибута Валидатеранже</span><span class="sxs-lookup"><span data-stu-id="0f87b-111">ValidateRange Attribute Declaration</span></span>](./validaterange-attribute-declaration.md)

[<span data-ttu-id="0f87b-112">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f87b-112">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)