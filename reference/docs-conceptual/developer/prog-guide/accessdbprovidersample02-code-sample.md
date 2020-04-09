---
title: Пример кода AccessDbProviderSample02 | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b89a4903-3efc-4b08-9b20-2baadf1d1b66
caps.latest.revision: 6
ms.openlocfilehash: 32abcfafb207ada23667cc6f0f03d382c6868ccb
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80978616"
---
# <a name="accessdbprovidersample02-code-sample"></a><span data-ttu-id="93b20-102">Пример кода AccessDbProviderSample02</span><span class="sxs-lookup"><span data-stu-id="93b20-102">AccessDbProviderSample02 Code Sample</span></span>

<span data-ttu-id="93b20-103">В следующем коде показана реализация поставщика Windows PowerShell, описанного в статье [Создание поставщика диска Windows PowerShell](./creating-a-windows-powershell-drive-provider.md).</span><span class="sxs-lookup"><span data-stu-id="93b20-103">The following code shows the implementation of the Windows PowerShell provider described in [Creating a Windows PowerShell Drive Provider](./creating-a-windows-powershell-drive-provider.md).</span></span>
<span data-ttu-id="93b20-104">Эта реализация создает путь, устанавливает соединение с базой данных Access, а затем удаляет диск.</span><span class="sxs-lookup"><span data-stu-id="93b20-104">This implementation creates a path, makes a connection to an Access database, and then removes the drive.</span></span>

> [!NOTE]
> <span data-ttu-id="93b20-105">C# Исходный файл (AccessDBSampleProvider02.cs) для этого поставщика можно скачать с помощью пакета средств разработки программного обеспечения Microsoft Windows для компонентов среды выполнения Windows Vista и Microsoft .NET Framework 3,0.</span><span class="sxs-lookup"><span data-stu-id="93b20-105">You can download the C# source file (AccessDBSampleProvider02.cs) for this provider using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="93b20-106">Инструкции по загрузке см. в статье [Установка Windows PowerShell и Загрузка пакета SDK для Windows PowerShell](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="93b20-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/scripting/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="93b20-107">Скачанные исходные файлы доступны в **\<примеров PowerShell >** Directory.</span><span class="sxs-lookup"><span data-stu-id="93b20-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span> <span data-ttu-id="93b20-108">Дополнительные сведения о других реализациях поставщиков Windows PowerShell см. в разделе [Разработка поставщика Windows PowerShell](./designing-your-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="93b20-108">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="93b20-109">Образец кода</span><span class="sxs-lookup"><span data-stu-id="93b20-109">Code Sample</span></span>

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="11-154":::

## <a name="see-also"></a><span data-ttu-id="93b20-110">См. также:</span><span class="sxs-lookup"><span data-stu-id="93b20-110">See Also</span></span>

[<span data-ttu-id="93b20-111">Руководством программиста Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="93b20-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="93b20-112">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="93b20-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
