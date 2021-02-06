---
external help file: PSModule-help.xml
Locale: en-US
Module Name: PowerShellGet
ms.date: 06/04/2019
online version: https://docs.microsoft.com/powershell/module/powershellget/find-dscresource?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Find-DscResource
ms.openlocfilehash: e1cb814d349d6b77885ebaaf176a7c3153d93eb5
ms.sourcegitcommit: 22c93550c87af30c4895fcb9e9dd65e30d60ada0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/19/2020
ms.locfileid: "99601591"
---
# <span data-ttu-id="743db-102">Find-DscResource</span><span class="sxs-lookup"><span data-stu-id="743db-102">Find-DscResource</span></span>

## <span data-ttu-id="743db-103">Краткий обзор</span><span class="sxs-lookup"><span data-stu-id="743db-103">SYNOPSIS</span></span>
<span data-ttu-id="743db-104">Находит ресурсы настройки требуемого состояния (DSC).</span><span class="sxs-lookup"><span data-stu-id="743db-104">Finds Desired State Configuration (DSC) resources.</span></span>

## <span data-ttu-id="743db-105">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="743db-105">SYNTAX</span></span>

### <span data-ttu-id="743db-106">Все</span><span class="sxs-lookup"><span data-stu-id="743db-106">All</span></span>

```
Find-DscResource [[-Name] <String[]>] [-ModuleName <String>] [-MinimumVersion <String>]
 [-MaximumVersion <String>] [-RequiredVersion <String>] [-AllVersions] [-AllowPrerelease]
 [-Tag <String[]>] [-Filter <String>] [-Proxy <Uri>] [-ProxyCredential <PSCredential>]
 [-Repository <String[]>] [<CommonParameters>]
```

## <span data-ttu-id="743db-107">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="743db-107">DESCRIPTION</span></span>

<span data-ttu-id="743db-108">`Find-DscResource`Командлет ищет зарегистрированные репозитории для поиска ресурсов DSC, содержащихся в модулях.</span><span class="sxs-lookup"><span data-stu-id="743db-108">The `Find-DscResource` cmdlet searches registered repositories to find DSC resources contained in modules.</span></span> <span data-ttu-id="743db-109">По умолчанию `Find-DscResource` Поиск выполняется по всем зарегистрированным репозиториям.</span><span class="sxs-lookup"><span data-stu-id="743db-109">By default `Find-DscResource` searches all registered repositories.</span></span>

<span data-ttu-id="743db-110">Для каждого модуля, найденного `Find-DscResource` , возвращается объект **псжетдскресаурцеинфо** .</span><span class="sxs-lookup"><span data-stu-id="743db-110">For each module found by `Find-DscResource`, a **PSGetDscResourceInfo** object is returned.</span></span>
<span data-ttu-id="743db-111">Объекты **псжетдскресаурцеинфо** можно отсылать по конвейеру в `Install-Module` командлет.</span><span class="sxs-lookup"><span data-stu-id="743db-111">**PSGetDscResourceInfo** objects can be sent down the pipeline to the `Install-Module` cmdlet.</span></span>
<span data-ttu-id="743db-112">`Install-Module` устанавливает модуль.</span><span class="sxs-lookup"><span data-stu-id="743db-112">`Install-Module` installs the module.</span></span>

## <span data-ttu-id="743db-113">Примеры</span><span class="sxs-lookup"><span data-stu-id="743db-113">EXAMPLES</span></span>

### <span data-ttu-id="743db-114">Пример 1. Поиск всех ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="743db-114">Example 1: Find all DSC resources</span></span>

<span data-ttu-id="743db-115">`Find-DscResource` Возвращает ресурсы DSC из зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="743db-115">`Find-DscResource` returns DSC resources from registered repositories.</span></span> <span data-ttu-id="743db-116">Для поиска в определенном репозитории используйте параметр **репозитория** .</span><span class="sxs-lookup"><span data-stu-id="743db-116">To search a specific repository, use the **Repository** parameter.</span></span>

```powershell
Find-DscResource
```

```Output
Name                           Version    ModuleName                     Repository
----                           -------    ----------                     ----------
Carbon_Privilege               2.8.1      Carbon                         PSGallery
Carbon_ScheduledTask           2.8.1      Carbon                         PSGallery
Carbon_Service                 2.8.1      Carbon                         PSGallery
PackageManagement              1.4        PackageManagement              PSGallery
PackageManagementSource        1.4        PackageManagement              PSGallery
PSModule                       2.1.4      PowerShellGet                  PSGallery
PSRepository                   2.1.4      PowerShellGet                  PSGallery
xArchive                       8.7.0.0    xPSDesiredStateConfiguration   PSGallery
xDSCWebService                 8.7.0.0    xPSDesiredStateConfiguration   PSGallery
xEnvironment                   8.7.0.0    xPSDesiredStateConfiguration   PSGallery
```

### <span data-ttu-id="743db-117">Пример 2. поиск ресурса DSC по имени</span><span class="sxs-lookup"><span data-stu-id="743db-117">Example 2: Find a DSC resource by name</span></span>

<span data-ttu-id="743db-118">`Find-DscResource` находит ресурсы DSC по имени.</span><span class="sxs-lookup"><span data-stu-id="743db-118">`Find-DscResource` locates DSC resources by name.</span></span> <span data-ttu-id="743db-119">Используйте запятые для разделения массива имен ресурсов.</span><span class="sxs-lookup"><span data-stu-id="743db-119">Use commas to separate an array of resource names.</span></span>

```powershell
Find-DscResource -Name xWebsite, xWebApplication, xWebSiteDefaults
```

```Output
Name               Version    ModuleName            Repository
----               -------    ----------            ----------
xWebApplication    2.6.0.0    xWebAdministration    PSGallery
xWebsite           2.6.0.0    xWebAdministration    PSGallery
xWebSiteDefaults   2.6.0.0    xWebAdministration    PSGallery
```

<span data-ttu-id="743db-120">`Find-DscResource` использует параметр **Name** для поиска указанного массива ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="743db-120">`Find-DscResource` uses the **Name** parameter to find the specified array of DSC resources.</span></span>

### <span data-ttu-id="743db-121">Пример 3. поиск ресурса DSC и его установка</span><span class="sxs-lookup"><span data-stu-id="743db-121">Example 3: Find a DSC resource and install it</span></span>

<span data-ttu-id="743db-122">`Find-DscResource` находит ресурс DSC и отправляет объект по конвейеру, который необходимо установить.</span><span class="sxs-lookup"><span data-stu-id="743db-122">`Find-DscResource` locates a DSC resource and sends the object down the pipeline to be installed.</span></span>
<span data-ttu-id="743db-123">После установки используйте `Get-InstalledModule` для просмотра результатов.</span><span class="sxs-lookup"><span data-stu-id="743db-123">After the installation, use `Get-InstalledModule` to view the results.</span></span>

<span data-ttu-id="743db-124">Несколько ресурсов из одного модуля можно отсылать по конвейеру в `Install-Module` .</span><span class="sxs-lookup"><span data-stu-id="743db-124">Multiple resources from the same module can be sent down the pipeline to the `Install-Module`.</span></span>
<span data-ttu-id="743db-125">`Install-Module` пытается установить модуль только один раз.</span><span class="sxs-lookup"><span data-stu-id="743db-125">`Install-Module` attempts to only install the module once.</span></span>

```powershell
Find-DscResource -Name xWebsite | Install-Module
```

<span data-ttu-id="743db-126">`Find-DscResource` использует параметр **Name** для поиска ресурса с именем **ксвебсите**.</span><span class="sxs-lookup"><span data-stu-id="743db-126">`Find-DscResource` uses the **Name** parameter to find the resource named **xWebsite**.</span></span> <span data-ttu-id="743db-127">Объект отправляется по конвейеру в `Install-Module` командлет.</span><span class="sxs-lookup"><span data-stu-id="743db-127">The object is sent down the pipeline to the `Install-Module` cmdlet.</span></span> <span data-ttu-id="743db-128">`Install-Module` устанавливает модуль **xWebAdministration** для ресурса.</span><span class="sxs-lookup"><span data-stu-id="743db-128">`Install-Module` installs the **xWebAdministration** module for the resource.</span></span>

### <span data-ttu-id="743db-129">Пример 4. Поиск всех ресурсов DSC в модуле</span><span class="sxs-lookup"><span data-stu-id="743db-129">Example 4: Find all DSC resources in a module</span></span>

<span data-ttu-id="743db-130">`Find-DscResource` находит все ресурсы DSC, содержащиеся в указанном модуле.</span><span class="sxs-lookup"><span data-stu-id="743db-130">`Find-DscResource` finds all the DSC resources contained in a specified module.</span></span> <span data-ttu-id="743db-131">По умолчанию отображается текущая версия.</span><span class="sxs-lookup"><span data-stu-id="743db-131">By default, the current version is displayed.</span></span> <span data-ttu-id="743db-132">Чтобы отобразить другие версии, используйте параметры **AllVersions** или **рекуиредверсионс** .</span><span class="sxs-lookup"><span data-stu-id="743db-132">To display other versions, use the **AllVersions** or **RequiredVersions** parameters.</span></span>

```powershell
Find-DscResource -ModuleName xWebAdministration
```

```Output
Name                                Version    ModuleName              Repository
----                                -------    ----------              ----------
WebApplicationHandler               2.6.0.0    xWebAdministration      PSGallery
xIisFeatureDelegation               2.6.0.0    xWebAdministration      PSGallery
xIisHandler                         2.6.0.0    xWebAdministration      PSGallery
xIisLogging                         2.6.0.0    xWebAdministration      PSGallery
```

<span data-ttu-id="743db-133">`Find-DscResource` использует параметр **ModuleName** для указания **xWebAdministration** и поиска ресурсов DSC, содержащихся в модуле.</span><span class="sxs-lookup"><span data-stu-id="743db-133">`Find-DscResource` uses the **ModuleName** parameter to specify the **xWebAdministration** and find the DSC resources contained in the module.</span></span> <span data-ttu-id="743db-134">Отобразится текущая версия каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="743db-134">The current version of each resource is displayed.</span></span>

### <span data-ttu-id="743db-135">Пример 5. поиск ресурса DSC по тегу и требуемой версии</span><span class="sxs-lookup"><span data-stu-id="743db-135">Example 5: Find a DSC resource by tag and required version</span></span>

<span data-ttu-id="743db-136">Ресурсы DSC можно найти с помощью **тега** параметров и **RequiredVersion**.</span><span class="sxs-lookup"><span data-stu-id="743db-136">DSC resources can be located using the parameters **Tag** and **RequiredVersion**.</span></span> <span data-ttu-id="743db-137">**Тег** отображает текущую версию каждого ресурса, содержащего указанный тег в репозитории.</span><span class="sxs-lookup"><span data-stu-id="743db-137">**Tag** displays the current version of every resource that contains the specified tag in the repository.</span></span>
<span data-ttu-id="743db-138">**RequiredVersion** требуется параметр **ModuleName** , а параметр **Name** — необязательный.</span><span class="sxs-lookup"><span data-stu-id="743db-138">**RequiredVersion** needs the **ModuleName** parameter and the **Name** parameter is optional.</span></span> <span data-ttu-id="743db-139">Параметры **Name** и **ModuleName** ограничивают выходные данные.</span><span class="sxs-lookup"><span data-stu-id="743db-139">The **Name** and **ModuleName** parameters limit the output.</span></span> <span data-ttu-id="743db-140">Используйте параметр **AllVersions** для вывода доступных версий ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="743db-140">Use the **AllVersions** parameter to display a DSC resource's available versions.</span></span>

```powershell
Find-DscResource -ModuleName xWebAdministration -Tag DSC -RequiredVersion 1.20
```

```output
Name                    Version    ModuleName             Repository
----                    -------    ----------             ----------
xIisFeatureDelegation   1.20.0.0   xWebAdministration     PSGallery
xIisHandler             1.20.0.0   xWebAdministration     PSGallery
xIisLogging             1.20.0.0   xWebAdministration     PSGallery
xIisMimeTypeMapping     1.20.0.0   xWebAdministration     PSGallery
```

### <span data-ttu-id="743db-141">Пример 6. поиск ресурса с помощью фильтра</span><span class="sxs-lookup"><span data-stu-id="743db-141">Example 6: Find a resource by using a filter</span></span>

<span data-ttu-id="743db-142">`Find-DscResource` находит все ресурсы и использует параметр **Filter** для указания результатов по **домену**.</span><span class="sxs-lookup"><span data-stu-id="743db-142">`Find-DscResource` finds all resources and uses the **Filter** parameter to specify the results by **Domain**.</span></span> <span data-ttu-id="743db-143">Параметр **Filter** находит значение фильтра в описании объекта или имени модуля.</span><span class="sxs-lookup"><span data-stu-id="743db-143">The **Filter** parameter finds the filter value in the object's description or module name.</span></span> <span data-ttu-id="743db-144">Используйте `Select-Object` командлет для просмотра свойств объекта.</span><span class="sxs-lookup"><span data-stu-id="743db-144">Use the `Select-Object` cmdlet to view an object's properties.</span></span>

```powershell
Find-DscResource -Filter Domain
```

```output
Name                    Version    ModuleName                 Repository
----                    -------    ----------                 ---------
xComputer               4.1.0.0    xComputerManagement        PSGallery
Computer                6.4.0.0    ComputerManagementDsc      PSGallery
xDSCDomainjoin          1.1        xDSCDomainjoin             PSGallery
xDisk                   1.0        xDisk                      PSGallery
xDSCFirewall            1.6.21     xDSCFirewall               PSGallery
dmAwsTagInstance        1.0.1      domainAwsDSCResources      PSGallery
```

## <span data-ttu-id="743db-145">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="743db-145">PARAMETERS</span></span>

### <span data-ttu-id="743db-146">-AllowPrerelease</span><span class="sxs-lookup"><span data-stu-id="743db-146">-AllowPrerelease</span></span>

<span data-ttu-id="743db-147">Включает ресурсы, помеченные как предварительные версии в результатах.</span><span class="sxs-lookup"><span data-stu-id="743db-147">Includes resources marked as a prerelease in the results.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-148">-AllVersions</span><span class="sxs-lookup"><span data-stu-id="743db-148">-AllVersions</span></span>

<span data-ttu-id="743db-149">Параметр **AllVersions** отображает все доступные версии ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="743db-149">The **AllVersions** parameter displays each of a DSC resource's available versions.</span></span> <span data-ttu-id="743db-150">Параметр **AllVersions** нельзя использовать с параметрами **MinimumVersion**, **MaximumVersion** или **RequiredVersion** .</span><span class="sxs-lookup"><span data-stu-id="743db-150">You can't use the **AllVersions** parameter with the **MinimumVersion**, **MaximumVersion**, or **RequiredVersion** parameters.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-151">-Filter</span><span class="sxs-lookup"><span data-stu-id="743db-151">-Filter</span></span>

<span data-ttu-id="743db-152">Находит ресурсы на основе синтаксиса поиска поставщика **PackageManagement** .</span><span class="sxs-lookup"><span data-stu-id="743db-152">Finds resources based on the **PackageManagement** provider's search syntax.</span></span> <span data-ttu-id="743db-153">Например, укажите слова для поиска в свойствах **ModuleName** и **Description** .</span><span class="sxs-lookup"><span data-stu-id="743db-153">For example, specify words to search for within the **ModuleName** and **Description** properties.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-154">-MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="743db-154">-MaximumVersion</span></span>

<span data-ttu-id="743db-155">Указывает максимальную версию ресурса, включаемую в результаты.</span><span class="sxs-lookup"><span data-stu-id="743db-155">Specifies the maximum version of the resource to include in results.</span></span> <span data-ttu-id="743db-156">Параметры **MaximumVersion** и **RequiredVersion** нельзя использовать в одной команде.</span><span class="sxs-lookup"><span data-stu-id="743db-156">The **MaximumVersion** and the **RequiredVersion** parameters can't be used in the same command.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-157">-MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="743db-157">-MinimumVersion</span></span>

<span data-ttu-id="743db-158">Указывает минимальную версию ресурса для включения в результаты.</span><span class="sxs-lookup"><span data-stu-id="743db-158">Specifies the minimum version of the resource to include in results.</span></span> <span data-ttu-id="743db-159">Параметры **MinimumVersion** и **RequiredVersion** нельзя использовать в одной команде.</span><span class="sxs-lookup"><span data-stu-id="743db-159">The **MinimumVersion** and the **RequiredVersion** parameters can't be used in the same command.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-160">-ModuleName</span><span class="sxs-lookup"><span data-stu-id="743db-160">-ModuleName</span></span>

<span data-ttu-id="743db-161">Указывает модуль, содержащий ресурс DSC.</span><span class="sxs-lookup"><span data-stu-id="743db-161">Specifies a module that contains the DSC resource.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-162">-Name</span><span class="sxs-lookup"><span data-stu-id="743db-162">-Name</span></span>

<span data-ttu-id="743db-163">Указывает имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="743db-163">Specifies the name of a resource.</span></span> <span data-ttu-id="743db-164">По умолчанию все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="743db-164">The default is all resources.</span></span> <span data-ttu-id="743db-165">Используйте запятые для разделения массива имен ресурсов.</span><span class="sxs-lookup"><span data-stu-id="743db-165">Use commas to separate an array of resource names.</span></span>

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-166">Прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="743db-166">-Proxy</span></span>

<span data-ttu-id="743db-167">Указывает прокси-сервер для запроса, а не прямое подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="743db-167">Specifies a proxy server for the request, rather than a direct connection to the internet resource.</span></span>

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="743db-168">-ProxyCredential</span><span class="sxs-lookup"><span data-stu-id="743db-168">-ProxyCredential</span></span>

<span data-ttu-id="743db-169">Указывает учетную запись пользователя с разрешением на использование прокси-сервера, указанного в параметре **прокси** .</span><span class="sxs-lookup"><span data-stu-id="743db-169">Specifies a user account with permission to use the proxy server specified in the **Proxy** parameter.</span></span>

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="743db-170">— Репозиторий;</span><span class="sxs-lookup"><span data-stu-id="743db-170">-Repository</span></span>

<span data-ttu-id="743db-171">Указывает репозиторий для поиска ресурсов.</span><span class="sxs-lookup"><span data-stu-id="743db-171">Specifies a repository to search for resources.</span></span> <span data-ttu-id="743db-172">Используйте запятые для разделения массива имен репозитория.</span><span class="sxs-lookup"><span data-stu-id="743db-172">Use commas to separate an array of repository names.</span></span>

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-173">-RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="743db-173">-RequiredVersion</span></span>

<span data-ttu-id="743db-174">Указывает точный номер версии модуля для включения в результаты.</span><span class="sxs-lookup"><span data-stu-id="743db-174">Specifies the module's exact version number to include in the results.</span></span> <span data-ttu-id="743db-175">Параметры **RequiredVersion** и **MinimumVersion** нельзя использовать в одной команде.</span><span class="sxs-lookup"><span data-stu-id="743db-175">The **RequiredVersion** and the **MinimumVersion** parameters can't be used in the same command.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-176">-Tag</span><span class="sxs-lookup"><span data-stu-id="743db-176">-Tag</span></span>

<span data-ttu-id="743db-177">Указывает теги, которые классифицируют модули в репозитории.</span><span class="sxs-lookup"><span data-stu-id="743db-177">Specifies tags that categorize modules in a repository.</span></span> <span data-ttu-id="743db-178">Используйте запятые для разделения массива тегов.</span><span class="sxs-lookup"><span data-stu-id="743db-178">Use commas to separate an array of tags.</span></span>

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="743db-179">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="743db-179">CommonParameters</span></span>

<span data-ttu-id="743db-180">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="743db-180">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="743db-181">См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="743db-181">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="743db-182">Входные данные</span><span class="sxs-lookup"><span data-stu-id="743db-182">INPUTS</span></span>

## <span data-ttu-id="743db-183">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="743db-183">OUTPUTS</span></span>

### <span data-ttu-id="743db-184">псжетдскресаурцеинфо</span><span class="sxs-lookup"><span data-stu-id="743db-184">PSGetDscResourceInfo</span></span>

<span data-ttu-id="743db-185">`Find-DscResource` Возвращает объект **псжетдскресаурцеинфо** .</span><span class="sxs-lookup"><span data-stu-id="743db-185">`Find-DscResource` returns a **PSGetDscResourceInfo** object.</span></span>

## <span data-ttu-id="743db-186">ПРИМЕЧАНИЯ</span><span class="sxs-lookup"><span data-stu-id="743db-186">NOTES</span></span>

> [!IMPORTANT]
> <span data-ttu-id="743db-187">Начиная с апреля 2020 года коллекция PowerShell не поддерживает протокол TLS (Transport Layer Security) версий 1.0 и 1.1.</span><span class="sxs-lookup"><span data-stu-id="743db-187">As of April 2020, the PowerShell Gallery no longer supports Transport Layer Security (TLS) versions 1.0 and 1.1.</span></span> <span data-ttu-id="743db-188">Если вы не используете TLS 1.2 или более поздней версии, при попытке доступа к коллекции PowerShell возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="743db-188">If you are not using TLS 1.2 or higher, you will receive an error when trying to access the PowerShell Gallery.</span></span> <span data-ttu-id="743db-189">Чтобы проверить, используется ли TLS 1.2, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="743db-189">Use the following command to ensure you are using TLS 1.2:</span></span>
>
> `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12`
>
> <span data-ttu-id="743db-190">Дополнительные сведения см. в [объявлении](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) в блоге, посвященном PowerShell.</span><span class="sxs-lookup"><span data-stu-id="743db-190">For more information, see the [announcement](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) in the PowerShell blog.</span></span>

## <span data-ttu-id="743db-191">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="743db-191">RELATED LINKS</span></span>

[<span data-ttu-id="743db-192">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="743db-192">Get-InstalledModule</span></span>](Get-InstalledModule.md)

[<span data-ttu-id="743db-193">Install-Module</span><span class="sxs-lookup"><span data-stu-id="743db-193">Install-Module</span></span>](Install-Module.md)

[<span data-ttu-id="743db-194">Register-PSRepository</span><span class="sxs-lookup"><span data-stu-id="743db-194">Register-PSRepository</span></span>](Register-PSRepository.md)

[<span data-ttu-id="743db-195">Select-Object</span><span class="sxs-lookup"><span data-stu-id="743db-195">Select-Object</span></span>](../Microsoft.PowerShell.Utility/Select-Object.md)

[<span data-ttu-id="743db-196">Uninstall — Module</span><span class="sxs-lookup"><span data-stu-id="743db-196">Uninstall-Module</span></span>](Uninstall-Module.md)