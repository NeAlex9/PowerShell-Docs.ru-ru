---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 31fde15e644455dbe77f68bca713bf026544fdc7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55682774"
---
# <a name="on-demand-pull-of-dsc-configurations"></a><span data-ttu-id="95a17-102">Извлечение по запросу для конфигураций DSC</span><span class="sxs-lookup"><span data-stu-id="95a17-102">On-demand PULL of DSC Configurations</span></span>

<span data-ttu-id="95a17-103">Новый командлет Update-DscConfiguration активирует извлечение с опрашивающих серверов, определенных в метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="95a17-103">The new Update-DscConfiguration cmdlet triggers a pull from the pull server(s) defined in the meta-configuration.</span></span> <span data-ttu-id="95a17-104">Такое поведение часто называется "оперативным извлечением".</span><span class="sxs-lookup"><span data-stu-id="95a17-104">The behavior is often referred to as 'Pull Now'.</span></span>


<span data-ttu-id="95a17-105">После активации извлечение осуществляется точно так же, как и в обычном случае:</span><span class="sxs-lookup"><span data-stu-id="95a17-105">Once triggered, the pull behaves exactly the same as it would have when triggered during the regular frequency:</span></span>

1. <span data-ttu-id="95a17-106">Контрольная сумма для текущей конфигурации сравнивается с контрольной суммой конфигурации на опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="95a17-106">The checksum for current configuration is compared to the checksum for the configuration on the pull server.</span></span>
2. <span data-ttu-id="95a17-107">Если они совпадают, процедура завершается успешно без применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="95a17-107">If they are the same, it completes successfully without applying the configuration.</span></span>
3. <span data-ttu-id="95a17-108">Если они различаются, конфигурация извлекается с опрашивающего сервера и применяется.</span><span class="sxs-lookup"><span data-stu-id="95a17-108">If they are different, the configuration is pulled down from the pull server and applied.</span></span>

<span data-ttu-id="95a17-109">**Примечание.** Если Meta-Configuration RefreshMode = "Push", этот командлет возвращает ошибку, поэтому он всегда не выполняет никаких действий, когда целевой узел находится в режиме Push.</span><span class="sxs-lookup"><span data-stu-id="95a17-109">**Note:** If the Meta-Configuration RefreshMode = 'Push' an error is returned by this cmdlet so this cmdlet will always do nothing when a target node is in 'Push' Mode.</span></span>

```powershell
Update-DscConfiguration     [[-ComputerName] <string[]>]
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-Credential<pscredential>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]

Update-DscConfiguration     -CimSession <CimSession[]>
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]
```
