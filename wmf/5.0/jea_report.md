---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 2fb2e4b0c40322b5ec78fabede22a7e3ecbbd2aa
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093768"
---
# <a name="reporting-on-jea"></a><span data-ttu-id="c3ecd-102">Отчеты о JEA</span><span class="sxs-lookup"><span data-stu-id="c3ecd-102">Reporting on JEA</span></span>

<span data-ttu-id="c3ecd-103">Чтобы отправить отчета о состоянии конфигурации JEA, можно использовать следующее.</span><span class="sxs-lookup"><span data-stu-id="c3ecd-103">In order to report on the state of your JEA configuration, you can use:</span></span>

1. <span data-ttu-id="c3ecd-104">**Get-PSSessionConfiguration** для получения списка всех зарегистрированных конечных точек на заданном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c3ecd-104">**Get-PSSessionConfiguration** to return a list of all registered endpoints on a given machine.</span></span>
1. <span data-ttu-id="c3ecd-105">**Get-PSSessionCapability** для получения отчета о возможности любого пользователя на заданной конечной точке.</span><span class="sxs-lookup"><span data-stu-id="c3ecd-105">**Get-PSSessionCapability** to report on the capabilities any given user has on a specific endpoint.</span></span>

<span data-ttu-id="c3ecd-106">Ниже приведен пример использования **Get-PSSessionCapability**:</span><span class="sxs-lookup"><span data-stu-id="c3ecd-106">Here's an example of **Get-PSSessionCapability**:</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           clear -> Clear-Host
Alias           cls -> Clear-Host
Alias           exsn -> Exit-PSSession
Alias           gcm -> Get-Command
Alias           measure -> Measure-Object
Alias           select -> Select-Object
Function        Clear-Host
Function        Exit-PSSession
Function        Get-Command
Function        Get-FormatData
Function        Get-Help
Function        Get-UserInfo
Function        Measure-Object
Function        Out-Default
Function        Select-Object
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...
```

<span data-ttu-id="c3ecd-107">Чтобы отправить отчет о _действиях_, выполненных пользователем во время сеанса JEA, можно выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="c3ecd-107">To report on the _actions_ users took during a JEA session, you can:</span></span>
1. <span data-ttu-id="c3ecd-108">Включить записи с запросом на повышение прав для этой конечной точки JEA и обратиться к каталогу записей получения полного журнала действий каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3ecd-108">Enable the "over-the-shoulder" transcripts for that JEA endpoint and consult the transcript directory for a full log of each user's actions</span></span>
2. <span data-ttu-id="c3ecd-109">Включить ведение журнала модуля PowerShell и просмотреть журналы событий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3ecd-109">Turn on PowerShell module logging and inspect the PowerShell event logs.</span></span>
