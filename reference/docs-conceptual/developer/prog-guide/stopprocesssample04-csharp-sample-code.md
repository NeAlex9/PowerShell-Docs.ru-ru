---
title: Пример кодаC#StopProcessSample04 () | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 778ce1a2-e16d-4af5-b15b-77ca4326bdc4
caps.latest.revision: 5
ms.openlocfilehash: 52c0cedf237d05e874780d08887f91a87bf13ffd
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366463"
---
# <a name="stopprocesssample04-c-sample-code"></a><span data-ttu-id="0d071-102">Пример кода StopProcessSample04 (C#)</span><span class="sxs-lookup"><span data-stu-id="0d071-102">StopProcessSample04 (C#) Sample Code</span></span>

<span data-ttu-id="0d071-103">Ниже приведен полный C# пример кода для командлета StopProc04 Sample.</span><span class="sxs-lookup"><span data-stu-id="0d071-103">Here is the complete C# sample code for the StopProc04 sample cmdlet.</span></span> <span data-ttu-id="0d071-104">Это код для командлета `Stop-Process`, описанного в разделе [Добавление наборов параметров в командлет](../cmdlet/adding-parameter-sets-to-a-cmdlet.md).</span><span class="sxs-lookup"><span data-stu-id="0d071-104">This is the code for the `Stop-Process` cmdlet described in [Adding Parameter Sets to a Cmdlet](../cmdlet/adding-parameter-sets-to-a-cmdlet.md).</span></span> <span data-ttu-id="0d071-105">Командлет `Stop-Process` предназначен для завершения процессов, которые извлекаются с помощью командлета Get-proc (описывается в разделе [Создание первого командлета](../cmdlet/creating-a-cmdlet-without-parameters.md)).</span><span class="sxs-lookup"><span data-stu-id="0d071-105">The `Stop-Process` cmdlet is designed to stop processes that are retrieved using the Get-Proc cmdlet (described in [Creating Your First Cmdlet](../cmdlet/creating-a-cmdlet-without-parameters.md)).</span></span>

> [!NOTE]
> <span data-ttu-id="0d071-106">Вы можете скачать исходный C# файл (stopprocesssample04.cs) для этого командлета "прекращать-proc" с помощью пакета средств разработки программного обеспечения Microsoft Windows для компонентов среды выполнения Windows Vista и .NET Framework 3,0.</span><span class="sxs-lookup"><span data-stu-id="0d071-106">You can download the C# (stopprocesssample04.cs) source file for this Stop-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="0d071-107">Инструкции по загрузке см. в статье [Установка Windows PowerShell и Загрузка пакета SDK для Windows PowerShell](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="0d071-107">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="0d071-108">Скачанные исходные файлы доступны в каталоге **\<PowerShell samples >** Directory.</span><span class="sxs-lookup"><span data-stu-id="0d071-108">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

[!code-csharp[StopProcessSample04.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/StopProcessSample04/StopProcessSample04.cs#L11-L435 "StopProcessSample04.cs")]

## <a name="see-also"></a><span data-ttu-id="0d071-109">См. также:</span><span class="sxs-lookup"><span data-stu-id="0d071-109">See Also</span></span>

[<span data-ttu-id="0d071-110">Руководством программиста Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d071-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="0d071-111">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d071-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)