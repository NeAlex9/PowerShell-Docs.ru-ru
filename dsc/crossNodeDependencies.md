---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Указание межузловых зависимостей
ms.openlocfilehash: c1802d6baa1f2b3449603e0374a83e213abf598e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218626"
---
# <a name="specifying-cross-node-dependencies"></a><span data-ttu-id="08263-103">Указание межузловых зависимостей</span><span class="sxs-lookup"><span data-stu-id="08263-103">Specifying cross-node dependencies</span></span>

> <span data-ttu-id="08263-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="08263-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="08263-105">DSC предоставляет специальные ресурсы, **WaitForAll**, **WaitForAny** и **WaitForSome**, которые можно использовать в конфигурациях для указания зависимостей от конфигураций на других узлах.</span><span class="sxs-lookup"><span data-stu-id="08263-105">DSC provides special resources, **WaitForAll**, **WaitForAny**, and **WaitForSome** that can be used in configurations to specify dependencies on configurations on other nodes.</span></span> <span data-ttu-id="08263-106">Поведение этих ресурсов описано ниже.</span><span class="sxs-lookup"><span data-stu-id="08263-106">The behavior of these resources is as follows:</span></span>

* <span data-ttu-id="08263-107">**WaitForAll** — успешное выполнение, если указанный ресурс находится в нужном состоянии на всех целевых узлах, определенных в свойстве **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="08263-107">**WaitForAll**: Succeeds if the specified resource is in the desired state on all target nodes defined in the **NodeName** property.</span></span>
* <span data-ttu-id="08263-108">**WaitForAny** — успешное выполнение, если указанный ресурс находится в нужном состоянии как минимум на одном из целевых узлов, определенных в свойстве **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="08263-108">**WaitForAny**: Succeeds if the specified resource is in the desired state on at least one of the target nodes defined in the **NodeName** property.</span></span>
* <span data-ttu-id="08263-109">**WaitForSome** — указывает свойство **NodeCount** в дополнение к свойству **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="08263-109">**WaitForSome**: Specifies a **NodeCount** property in addition to a **NodeName** property.</span></span> <span data-ttu-id="08263-110">Ресурс выполняется успешно, если он находится в нужном состоянии на минимальном количестве узлов (определяется свойством **NodeCount**), заданных свойством **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="08263-110">The resource succeeds if the resource is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

## <a name="using-waitforxxxx-resources"></a><span data-ttu-id="08263-111">Использование ресурсов WaitForXXXX</span><span class="sxs-lookup"><span data-stu-id="08263-111">Using WaitForXXXX resources</span></span>

<span data-ttu-id="08263-112">Для использования ресурсов **WaitForXXXX** создается блок этого типа ресурса, указывающий ресурсы и узлы DSC для ожидания.</span><span class="sxs-lookup"><span data-stu-id="08263-112">To use the **WaitForXXXX** resources, you create a resource block of that resource type that specifies the DSC resource and node(s) to wait for.</span></span> <span data-ttu-id="08263-113">Затем используется свойство **DependsOn** в любых других блоках ресурсов в конфигурации для ожидания успешного выполнения условий, указанных в узле **WaitForXXXX**.</span><span class="sxs-lookup"><span data-stu-id="08263-113">You then use the **DependsOn** property in any other resource blocks in your configuration to wait for the conditions specified in the **WaitForXXXX** node to succeed.</span></span>

<span data-ttu-id="08263-114">Например, в следующей конфигурации целевой узел ожидает завершения выполнения ресурса **xADDomain** на узле **MyDC** не более чем с 30 повторными попытками (с интервалом 15 секунд), прежде чем присоединиться к домену.</span><span class="sxs-lookup"><span data-stu-id="08263-114">For example, in the following configuration, the target node is waiting for the **xADDomain** resource to finish on the **MyDC** node with maximum number of 30 retries, at 15-second intervals, before the target node can join the domain.</span></span>

```powershell
Configuration JoinDomain

{
    Import-DscResource -Module xComputerManagement, xActiveDirectory

    Node myDC
    {
        WindowsFeature InstallAD
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain NewDomain
        {
            DomainName = 'Contoso.com'
            DomainAdministratorCredential = (Get-Credential)
            SafemodeAdministratorPassword = (Get-Credential)
            DatabasePath = "C:\Windows\NTDS"
            LogPath = "C:\Windows\NTDS"
            SysvolPath = "C:\Windows\Sysvol"
        }

    }

    Node myDomainJoinedServer
    {

        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'myPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

><span data-ttu-id="08263-115">**Примечание.** По умолчанию ресурсы WaitForXXX выполняют одну попытку, а затем выдают ошибку.</span><span class="sxs-lookup"><span data-stu-id="08263-115">**Note:** By default the WaitForXXX resources try one time and then fail.</span></span> <span data-ttu-id="08263-116">Хотя это необязательно, обычно требуется указать интервал и число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="08263-116">Although it is not required, you will typically want to specify a retry interval and count.</span></span>

## <a name="see-also"></a><span data-ttu-id="08263-117">См. также</span><span class="sxs-lookup"><span data-stu-id="08263-117">See Also</span></span>
* [<span data-ttu-id="08263-118">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="08263-118">DSC Configurations</span></span>](configurations.md)
* [<span data-ttu-id="08263-119">Ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="08263-119">DSC Resources</span></span>](resources.md)
* [<span data-ttu-id="08263-120">Настройка локального диспетчера конфигураций</span><span class="sxs-lookup"><span data-stu-id="08263-120">Configuring The Local Configuration Manager</span></span>](metaConfig.md)