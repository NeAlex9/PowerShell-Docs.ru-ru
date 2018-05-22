---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 9efc640dfda7e08e59d2c56746facd9658b1f9de
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a>Обнаружение, установка и инвентаризация модуля PowerShell с помощью PowerShellGet

PowerShellGet входит в состав этого выпуска WMF:
-   Find-Module позволяет фильтровать метаданные модуля с помощью параметра -Tag.
-   Find-Module позволяет фильтровать язык поиска для определенного репозитория с помощью параметра -Filter.
-   Find-Module позволяет фильтровать содержимое модуля с помощью параметров -Command, -DscResource и -Includes.
-   Find-DscResource позволяет обнаруживать отдельные ресурсы DSC в репозитории.
-   Поддержка установки из общих папок и публикации в них с помощью NuGet

## <a name="example-commands"></a>Примеры команд
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a>Новые функции в PowerShellGet
-   Поддержка параллельных версий в Windows PowerShell 5.0 или более поздней версии
-   Поддержка установки зависимостей модулей
-   Три новых командлета
    -   Get-InstalledModule
    -   Uninstall-Module
    -   Save-Module
