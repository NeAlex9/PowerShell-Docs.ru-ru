---
title: RunSpace03 (C#) образец кода | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ac8ab99-1856-4d6f-b30d-c0a18b8dd1fc
caps.latest.revision: 6
ms.openlocfilehash: 0e80f4d850a7c6dc044526a56b92f16eea4040b5
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429913"
---
# <a name="runspace03-c-code-sample"></a><span data-ttu-id="1290e-102">Пример кода RunSpace03 (C#)</span><span class="sxs-lookup"><span data-stu-id="1290e-102">RunSpace03 (C#) Code Sample</span></span>

<span data-ttu-id="1290e-103">Вот C# исходный код для консольного приложения, описанные в [Создание консольного приложения, запускающегося сценария указан](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).</span><span class="sxs-lookup"><span data-stu-id="1290e-103">Here is the C# source code for the console application described in [Creating a Console Application That Runs a Specified Script](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).</span></span> <span data-ttu-id="1290e-104">В этом примере используется [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) класса, чтобы выполнить скрипт, который извлекает обработки информации, используя список имен процессов передачи в сценарий.</span><span class="sxs-lookup"><span data-stu-id="1290e-104">This sample uses the [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) class to execute a script that retrieves process information by using the list of process names passed into the script.</span></span> <span data-ttu-id="1290e-105">Он показывает, как для передачи входных объектов скрипта и как получить объекты ошибок, а также выходных объектов.</span><span class="sxs-lookup"><span data-stu-id="1290e-105">It shows how to pass input objects to a script and how to retrieve error objects as well as the output objects.</span></span>

> [!NOTE]
> <span data-ttu-id="1290e-106">Вы можете скачать C# исходный файл (runspace03.cs) для этого образца, используя Microsoft Windows программное обеспечение Development Kit для Windows Vista и компоненты среды выполнения Microsoft .NET Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="1290e-106">You can download the C# source file (runspace03.cs) for this sample using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="1290e-107">Инструкции по загрузке см. в разделе [как установка Windows PowerShell и загрузки пакета SDK для Windows PowerShell](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="1290e-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="1290e-108">Скачанный исходные файлы доступны в  **\<примеры PowerShell >** каталога.</span><span class="sxs-lookup"><span data-stu-id="1290e-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="1290e-109">Пример кода</span><span class="sxs-lookup"><span data-stu-id="1290e-109">Code Sample</span></span>

[!code-csharp[Runspace03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace03/Runspace03.cs#L11-L88 "Runspace03.cs")]

## <a name="see-also"></a><span data-ttu-id="1290e-110">См. также</span><span class="sxs-lookup"><span data-stu-id="1290e-110">See Also</span></span>

[<span data-ttu-id="1290e-111">Руководство программиста Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1290e-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="1290e-112">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1290e-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)