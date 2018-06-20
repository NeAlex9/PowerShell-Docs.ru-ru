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
# <a name="specifying-cross-node-dependencies"></a>Указание межузловых зависимостей

> Область применения: Windows PowerShell 5.0

DSC предоставляет специальные ресурсы, **WaitForAll**, **WaitForAny** и **WaitForSome**, которые можно использовать в конфигурациях для указания зависимостей от конфигураций на других узлах. Поведение этих ресурсов описано ниже.

* **WaitForAll** — успешное выполнение, если указанный ресурс находится в нужном состоянии на всех целевых узлах, определенных в свойстве **NodeName**.
* **WaitForAny** — успешное выполнение, если указанный ресурс находится в нужном состоянии как минимум на одном из целевых узлов, определенных в свойстве **NodeName**.
* **WaitForSome** — указывает свойство **NodeCount** в дополнение к свойству **NodeName**. Ресурс выполняется успешно, если он находится в нужном состоянии на минимальном количестве узлов (определяется свойством **NodeCount**), заданных свойством **NodeName**.

## <a name="using-waitforxxxx-resources"></a>Использование ресурсов WaitForXXXX

Для использования ресурсов **WaitForXXXX** создается блок этого типа ресурса, указывающий ресурсы и узлы DSC для ожидания. Затем используется свойство **DependsOn** в любых других блоках ресурсов в конфигурации для ожидания успешного выполнения условий, указанных в узле **WaitForXXXX**.

Например, в следующей конфигурации целевой узел ожидает завершения выполнения ресурса **xADDomain** на узле **MyDC** не более чем с 30 повторными попытками (с интервалом 15 секунд), прежде чем присоединиться к домену.

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

>**Примечание.** По умолчанию ресурсы WaitForXXX выполняют одну попытку, а затем выдают ошибку. Хотя это необязательно, обычно требуется указать интервал и число повторных попыток.

## <a name="see-also"></a>См. также
* [Конфигурации DSC](configurations.md)
* [Ресурсы DSC](resources.md)
* [Настройка локального диспетчера конфигураций](metaConfig.md)