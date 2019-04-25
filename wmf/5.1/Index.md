---
ms.date: 08/12/2017
ms.topic: conceptual
keywords: wmf,powershell,установка
title: Заметки о выпуске WMF 5.1
ms.openlocfilehash: dd68f101e6f21256f966f7472dabc273a475a25e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057287"
---
# <a name="windows-management-framework-wmf-51"></a><span data-ttu-id="7aa67-103">Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="7aa67-103">Windows Management Framework (WMF) 5.1</span></span>

<span data-ttu-id="7aa67-104">WMF предоставляет пользователям возможность обновить существующие системы Windows до версий PowerShell, WMI, WinRM и Software Inventory Logging (SIL), которые были выпущены с Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="7aa67-104">WMF provides users with the ability to update existing Windows systems to the versions of PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>

<span data-ttu-id="7aa67-105">Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="7aa67-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="7aa67-106">Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.</span><span class="sxs-lookup"><span data-stu-id="7aa67-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="7aa67-107">Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.</span><span class="sxs-lookup"><span data-stu-id="7aa67-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="7aa67-108">Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.</span><span class="sxs-lookup"><span data-stu-id="7aa67-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="7aa67-109">Улучшения отладки для классов DSC и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7aa67-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="7aa67-110">Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="7aa67-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="7aa67-111">Ответы на разные запросы пользователей и решение проблем.</span><span class="sxs-lookup"><span data-stu-id="7aa67-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="7aa67-112">Дополнительные сведения о новых возможностях в этом выпуске см. в разделах, перечисленных в статье [Новые сценарии и функции](https://docs.microsoft.com/powershell/wmf/5.1/scenarios-features).</span><span class="sxs-lookup"><span data-stu-id="7aa67-112">To learn about what is new in this release, browse the topics listed under [New Scenarios and Features](https://docs.microsoft.com/powershell/wmf/5.1/scenarios-features).</span></span>

<span data-ttu-id="7aa67-113">В разделе [Установка и настройка](https://docs.microsoft.com/powershell/wmf/5.1/install-configure) перечисляются требования и предоставляются инструкции по установке для WMF.</span><span class="sxs-lookup"><span data-stu-id="7aa67-113">The [Install and Configure](https://docs.microsoft.com/powershell/wmf/5.1/install-configure) topic lists the requirements and provides installation instructions for WMF.</span></span>

<span data-ttu-id="7aa67-114">В разделе [Совместимость](https://docs.microsoft.com/powershell/wmf/5.1/compatibility) перечисляются версии WMF, которые можно установить на выпуски Windows.</span><span class="sxs-lookup"><span data-stu-id="7aa67-114">The [Compatibility](https://docs.microsoft.com/powershell/wmf/5.1/compatibility) topic lists which versions of WMF may be installed on which Windows releases.</span></span>

<span data-ttu-id="7aa67-115">В разделе [Совместимость продуктов](https://docs.microsoft.com/powershell/wmf/5.1/productincompat) перечисляются приложения Майкрософт, которые не утвердили использование WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="7aa67-115">[Product Compatibility](https://docs.microsoft.com/powershell/wmf/5.1/productincompat) lists the Microsoft applications that have not approved WMF 5.1 for use at this time.</span></span>

<span data-ttu-id="7aa67-116">Сведения для компонентов WMF можно найти в документации MSDN:</span><span class="sxs-lookup"><span data-stu-id="7aa67-116">Details for the components of WMF will be found in MSDN documentation:</span></span>

- [<span data-ttu-id="7aa67-117">PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="7aa67-117">PowerShell 5.1</span></span>](https://docs.microsoft.com/powershell/)
- <span data-ttu-id="7aa67-118">[WMI](https://msdn.microsoft.com/library/jj152383(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="7aa67-118">[WMI](https://msdn.microsoft.com/library/jj152383(v=vs.85).aspx)</span></span>
- <span data-ttu-id="7aa67-119">[WinRM](https://msdn.microsoft.com/library/aa384426(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="7aa67-119">[WinRM](https://msdn.microsoft.com/library/aa384426(v=vs.85).aspx)</span></span>
- <span data-ttu-id="7aa67-120">[Ведение журнала инвентаризации программного обеспечения](https://technet.microsoft.com/library/dn383584(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="7aa67-120">[Software Inventory Logging](https://technet.microsoft.com/library/dn383584(v=ws.11).aspx)</span></span>
