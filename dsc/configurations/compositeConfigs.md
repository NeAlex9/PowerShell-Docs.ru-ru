---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Вложение конфигураций
ms.openlocfilehash: 54162cd72d2d1e7773e3be636bfa681329854498
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080243"
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="852f1-103">Вложение конфигураций DSC</span><span class="sxs-lookup"><span data-stu-id="852f1-103">Nesting DSC configurations</span></span>

<span data-ttu-id="852f1-104">Вложенная конфигурация (также называемая составной конфигурацией) — это конфигурация, которая вызывается в составе другой конфигурации подобно ресурсу.</span><span class="sxs-lookup"><span data-stu-id="852f1-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="852f1-105">Обе конфигурации должны быть определены в одном файле.</span><span class="sxs-lookup"><span data-stu-id="852f1-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="852f1-106">Давайте рассмотрим простой пример:</span><span class="sxs-lookup"><span data-stu-id="852f1-106">Let's look at a simple example:</span></span>

```powershell
Configuration FileConfig
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }

}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

<span data-ttu-id="852f1-107">В этом примере `FileConfig` принимает два обязательных параметра — **CopyFrom** и **CopyTo**, — которые используются как значения для свойств **SourcePath** и **DestinationPath** в блоке ресурсов `File`.</span><span class="sxs-lookup"><span data-stu-id="852f1-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="852f1-108">Конфигурация `NestedConfig` вызывает конфигурацию `FileConfig`, как будто это ресурс.</span><span class="sxs-lookup"><span data-stu-id="852f1-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="852f1-109">Свойства в блоке ресурсов `NestedConfig` (**CopyFrom** и **CopyTo**) — параметры конфигурации `FileConfig`.</span><span class="sxs-lookup"><span data-stu-id="852f1-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="852f1-110">См. также</span><span class="sxs-lookup"><span data-stu-id="852f1-110">See Also</span></span>

- [<span data-ttu-id="852f1-111">Составные ресурсы: использование DSC как ресурса</span><span class="sxs-lookup"><span data-stu-id="852f1-111">Composite resources--Using a DSC configuration as a resource</span></span>](../resources/authoringResourceComposite.md)