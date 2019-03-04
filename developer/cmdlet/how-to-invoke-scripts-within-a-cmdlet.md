---
title: Как будет вызывать скрипты в командлет | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cc0bc6ce-48a5-4d9c-927e-636bca743e9f
caps.latest.revision: 9
ms.openlocfilehash: 4b4d5645785b751eb1390e196f5b9437b4a1e13b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56855840"
---
# <a name="how-to-invoke-scripts-within-a-cmdlet"></a><span data-ttu-id="0dc6e-102">Как вызвать сценарий из командлета</span><span class="sxs-lookup"><span data-stu-id="0dc6e-102">How to Invoke Scripts Within a Cmdlet</span></span>

<span data-ttu-id="0dc6e-103">В этом примере показано, как вызвать скрипт, который передается в командлет.</span><span class="sxs-lookup"><span data-stu-id="0dc6e-103">This example shows how to invoke a script that is supplied to a cmdlet.</span></span> <span data-ttu-id="0dc6e-104">Сценарий выполняется с помощью командлета, а его результаты возвращаются в командлет как коллекция [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) объектов.</span><span class="sxs-lookup"><span data-stu-id="0dc6e-104">The script is executed by the cmdlet, and its results are returned to the cmdlet as a collection of [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objects.</span></span>

## <a name="to-invoke-a-script-block"></a><span data-ttu-id="0dc6e-105">Для вызова блок сценария</span><span class="sxs-lookup"><span data-stu-id="0dc6e-105">To invoke a script block</span></span>

1. <span data-ttu-id="0dc6e-106">Команда проверяет, что блок сценария передан в командлет.</span><span class="sxs-lookup"><span data-stu-id="0dc6e-106">The command verifies that a script block was supplied to the cmdlet.</span></span> <span data-ttu-id="0dc6e-107">Если передан блок сценария, команда вызывает блок скрипта с его нужными параметрами.</span><span class="sxs-lookup"><span data-stu-id="0dc6e-107">If a script block was supplied, the command invokes the script block with its required parameters.</span></span>

    ```csharp
    if (script != null)
    {
      WriteDebug("Executing script block.");

      // Invoke the script block with the required arguments.
      Collection<PSObject> PSObjects =
                     script.Invoke(
                                   line,
                                   simpleMatch,
                                   caseSensitive
                                  );
    ```

2. <span data-ttu-id="0dc6e-108">Затем, скрипт выполняется перебор Возвращенная коллекция [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) объектов и выполнить необходимые операции.</span><span class="sxs-lookup"><span data-stu-id="0dc6e-108">Then, the script iterates through the returned collection of [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objects and perform the necessary operations.</span></span>

    ```c
    foreach (PSObject psObject in psObjects)
    {
      if (LanguagePrimitives.IsTrue(psObject))
      {
        result = new MatchInfo();
        result.Line = line;
        result.IgnoreCase = !caseSensitive;

        break;
      }
    }

    ```

## <a name="see-also"></a><span data-ttu-id="0dc6e-109">См. также</span><span class="sxs-lookup"><span data-stu-id="0dc6e-109">See Also</span></span>

[<span data-ttu-id="0dc6e-110">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dc6e-110">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)