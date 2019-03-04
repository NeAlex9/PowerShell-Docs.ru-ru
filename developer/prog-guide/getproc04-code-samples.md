---
title: Примеры кода GetProc04 | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c00afd46-758a-4aec-b865-2c9d8f6a17ad
caps.latest.revision: 5
ms.openlocfilehash: d679bc8cbdb026e072628d3e0c5704de2eec7af9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56855450"
---
# <a name="getproc04-code-samples"></a><span data-ttu-id="5c5d9-102">Примеры кода GetProc04</span><span class="sxs-lookup"><span data-stu-id="5c5d9-102">GetProc04 Code Samples</span></span>

<span data-ttu-id="5c5d9-103">Ниже приведены примеры кода для командлета GetProc04 образца.</span><span class="sxs-lookup"><span data-stu-id="5c5d9-103">Here are the code samples for the GetProc04 sample cmdlet.</span></span> <span data-ttu-id="5c5d9-104">Это `Get-Process` командлетов, которые описаны в [Добавление устранимые отчеты об ошибках Your командлету](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md).</span><span class="sxs-lookup"><span data-stu-id="5c5d9-104">This is the `Get-Process` cmdlet sample described in [Adding Nonterminating Error Reporting to Your Cmdlet](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md).</span></span> <span data-ttu-id="5c5d9-105">Это `Get-Process` вызывает командлет [System.Management.Automation.Cmdlet.Writeerror\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) метод всякий раз, когда возникает исключение недопустимой операции при получении сведений о процессе.</span><span class="sxs-lookup"><span data-stu-id="5c5d9-105">This `Get-Process` cmdlet calls the [System.Management.Automation.Cmdlet.Writeerror\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method whenever an invalid operation exception is thrown while retrieving process information.</span></span>

> [!NOTE]
> <span data-ttu-id="5c5d9-106">Вы можете скачать C# исходный файл (getprov04.cs) для этого командлета Get-Proc, с помощью Microsoft Windows программное обеспечение Development Kit для Windows Vista и компоненты среды выполнения .NET Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="5c5d9-106">You can download the C# source file (getprov04.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="5c5d9-107">Инструкции по загрузке см. в разделе [как установка Windows PowerShell и загрузки пакета SDK для Windows PowerShell](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="5c5d9-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="5c5d9-108">Вы можете скачать C# исходный файл (getprov04.cs) для этого командлета Get-Proc, с помощью Microsoft Windows программное обеспечение Development Kit для Windows Vista и компоненты среды выполнения .NET Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="5c5d9-108">You can download the C# source file (getprov04.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="5c5d9-109">Инструкции по загрузке см. в разделе [как установка Windows PowerShell и загрузки пакета SDK для Windows PowerShell](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="5c5d9-109">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="5c5d9-110">Скачанный исходные файлы доступны в  **\<примеры PowerShell >** каталога.</span><span class="sxs-lookup"><span data-stu-id="5c5d9-110">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

<span data-ttu-id="5c5d9-111">Полный пример кода см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="5c5d9-111">For complete sample code, see the following topics.</span></span>

|<span data-ttu-id="5c5d9-112">Language</span><span class="sxs-lookup"><span data-stu-id="5c5d9-112">Language</span></span>|<span data-ttu-id="5c5d9-113">Раздел</span><span class="sxs-lookup"><span data-stu-id="5c5d9-113">Topic</span></span>|
|--------------|-----------|
|<span data-ttu-id="5c5d9-114">C#</span><span class="sxs-lookup"><span data-stu-id="5c5d9-114">C#</span></span>|[<span data-ttu-id="5c5d9-115">GetProc04 (C#) пример кода</span><span class="sxs-lookup"><span data-stu-id="5c5d9-115">GetProc04 (C#) Sample Code</span></span>](./getproc04-csharp-sample-code.md)|
|<span data-ttu-id="5c5d9-116">VB.NET</span><span class="sxs-lookup"><span data-stu-id="5c5d9-116">VB.NET</span></span>|[<span data-ttu-id="5c5d9-117">GetProc04 образец кода (VB.NET)</span><span class="sxs-lookup"><span data-stu-id="5c5d9-117">GetProc04 (VB.NET) Sample Code</span></span>](./getproc04-vb-net-sample-code.md)|

## <a name="see-also"></a><span data-ttu-id="5c5d9-118">См. также</span><span class="sxs-lookup"><span data-stu-id="5c5d9-118">See Also</span></span>

[<span data-ttu-id="5c5d9-119">Руководство программиста Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c5d9-119">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="5c5d9-120">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c5d9-120">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)