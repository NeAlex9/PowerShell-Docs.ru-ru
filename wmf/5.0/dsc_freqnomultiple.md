---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: a3ac215396206fba62bce303733429d60722ee6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218388"
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="4d577-102">Частоты для RefreshMode и ConfigurationMode не должны быть кратными друг другу</span><span class="sxs-lookup"><span data-stu-id="4d577-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="4d577-103">В предыдущей версии DSC локальный диспетчер конфигураций рассматривал `RefreshFrequencyMins` и `ConfigurationModeFrequencyMins` как кратные друг другу.</span><span class="sxs-lookup"><span data-stu-id="4d577-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="4d577-104">В WMF 5.0 RTM эти свойства обрабатываются независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="4d577-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span>

<span data-ttu-id="4d577-105">Дополнительные сведения см. в разделе [Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="4d577-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>
