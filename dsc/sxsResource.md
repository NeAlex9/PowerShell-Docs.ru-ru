---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Использование ресурсов с несколькими версиями
ms.openlocfilehash: 6400d6506106657ba28fa1f9c83d9f8ee1c93ba3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="using-resources-with-multiple-versions"></a>Использование ресурсов с несколькими версиями

> Область применения: Windows PowerShell 5.0

В PowerShell 5.0 ресурсы DSC могут иметь несколько версий, и эти версии можно устанавливать на компьютере параллельно. Это реализуется благодаря наличию нескольких версий модуля ресурсов, которые содержатся в одной папке модуля.

## <a name="installing-multiple-resource-versions-side-by-side"></a>Параллельная установка нескольких версий ресурса

Параметры **MinimumVersion**, **MaximumVersion** и **RequiredVersion** командлета [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) можно использовать, чтобы указать версию модуля для установки. Вызов командлета **Install-Module** без указания версии устанавливает последнюю версию.

Например, существует несколько версий модуля **xFailOverCluster**, каждая из которых содержит ресурс **xCluster**. Результат вызова командлета **Install-Module** без указания номера версии будет следующим.

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

Если снова вызвать командлет **Install-Module** и указать для параметра **RequiredVersion** значение 1.1.0.0, результат будет следующим:

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a>Указание версии ресурса в конфигурации

Если имеется несколько ресурсов, установленных на компьютере, необходимо указать версию нужного ресурса при его использовании в конфигурации. Это делается путем указания параметра **ModuleVersion** ключевого слова **Import-DscResource**. Если не указать версию модуля ресурсов для ресурса, имеющего несколько установленных версий, конфигурация породит ошибку.

В конфигурации ниже показано, как указать версию ресурса для вызова:

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

>Примечание. Параметр ModuleVersion ключевого слова Import-DscResource недоступен в PowerShell 4.0. В PowerShell 4.0 версию модуля можно задать, передав объект спецификации модуля в параметр ModuleName ключевого слова Import-DscResource. Объект спецификации модуля представляет собой хэш-таблицу, содержащую ключи ModuleName и RequiredVersion. Например:

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

Этот способ также будет работать в PowerShell 5.0, однако рекомендуется использовать параметр **ModuleVersion**.

## <a name="see-also"></a>См. также:
* [Конфигурации DSC](configurations.md)
* [Ресурсы DSC](resources.md)