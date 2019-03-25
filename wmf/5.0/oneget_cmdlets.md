---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 042e9a30068d32dc5860255bdec960371121d866
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795102"
---
# <a name="packagemanagement-cmdlets"></a><span data-ttu-id="fc170-102">Командлеты PackageManagement</span><span class="sxs-lookup"><span data-stu-id="fc170-102">PackageManagement Cmdlets</span></span>

<span data-ttu-id="fc170-103">Это основная составляющая PackageManagement, отвечающая за поддержку обнаружения, установки и инвентаризации программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="fc170-103">This is the core of PackageManagement to support software discovery, installation, and inventory (SDII).</span></span> <span data-ttu-id="fc170-104">Попробуйте использовать для выполнения этих операций следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="fc170-104">Try out the cmdlets for these operations:</span></span>

- `Find-Package`
- `Find-PackageProvider`
- `Get-Package`
- `Get-PackageProvider`
- `Get-PackageSource`
- `Import-PackageProvider`
- `Install-Package`
- `Install-PackageProvider`
- `Register-PackageSource`
- `Save-Package`
- `Set-PackageSource`
- `Uninstall-Package`
- `Unregister-PackageSource`

<span data-ttu-id="fc170-105">Поскольку PackageManagement является модулем PowerShell, можно обновить сам PackageManagement следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fc170-105">As PackageManagement is a PowerShell module, you can do the following to update PackageManagement itself:</span></span>

```powershell
Install-Module PackageManagement –Force
```

<span data-ttu-id="fc170-106">В этом случае потребуется повторно войти в сеанс PowerShell, чтобы переключиться на новую версию PackageManagement.</span><span class="sxs-lookup"><span data-stu-id="fc170-106">In this case, you will have to re-enter PowerShell session to switch to the new version of PackageManagement.</span></span>

## <a name="find-package-cmdletpowershellmodulepackagemanagementfind-package"></a>[<span data-ttu-id="fc170-107">Командлет Find-Package</span><span class="sxs-lookup"><span data-stu-id="fc170-107">Find-Package Cmdlet</span></span>](/powershell/module/PackageManagement/Find-Package)

<span data-ttu-id="fc170-108">Этот командлет обеспечивает обнаружения пакетов программного обеспечения в доступных источниках с помощью загруженных поставщиков пакетов.</span><span class="sxs-lookup"><span data-stu-id="fc170-108">This cmdlet allows discovery of software packages in available package sources using loaded package providers.</span></span>

```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -ProviderName PowerShellGet -Source as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## <a name="find-packageprovider-cmdletpowershellmodulepackagemanagementfind-packageprovider"></a>[<span data-ttu-id="fc170-109">Командлет Find-PackageProvider</span><span class="sxs-lookup"><span data-stu-id="fc170-109">Find-PackageProvider Cmdlet</span></span>](/powershell/module/PackageManagement/Find-PackageProvider)

<span data-ttu-id="fc170-110">Командлет `Find-PackageProvider` находит подходящие поставщики PackageManagement, которые доступны в зарегистрированных источниках пакетов PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="fc170-110">The `Find-PackageProvider` cmdlet finds matching PackageManagement providers that are available in package sources registered with PowerShellGet.</span></span> <span data-ttu-id="fc170-111">Эти поставщики пакетов можно установить с помощью командлета `Install-PackageProvider`.</span><span class="sxs-lookup"><span data-stu-id="fc170-111">These are package providers available for installation with the `Install-PackageProvider` cmdlet.</span></span> <span data-ttu-id="fc170-112">По умолчанию сюда относятся модули, доступные в коллекции PowerShell с тегами PackageManagement и Provider.</span><span class="sxs-lookup"><span data-stu-id="fc170-112">By default, this includes modules available in the PowerShell Gallery with the 'PackageManagement' and 'Provider' Tags.</span></span>

<span data-ttu-id="fc170-113">Кроме того, `Find-PackageProvider` находит совпадающие поставщики PackageManagement, доступные в хранилище BLOB-объектов Azure PackageManagement, где для их поиска и установки используется поставщик начального загрузчика PackageManagement.</span><span class="sxs-lookup"><span data-stu-id="fc170-113">`Find-PackageProvider` also finds matching PackageManagement providers that are available in the PackageManagement azure blob store where we use the PackageManagement boostrapper provider for finding and installing them.</span></span>

```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

## <a name="get-package-cmdletpowershellmodulepackagemanagementget-package"></a>[<span data-ttu-id="fc170-114">Командлет Get-Package</span><span class="sxs-lookup"><span data-stu-id="fc170-114">Get-Package Cmdlet</span></span>](/powershell/module/PackageManagement/Get-Package)

<span data-ttu-id="fc170-115">Этот командлет возвращает список всех пакетов программного обеспечения, установленных с помощью PackageManagement.</span><span class="sxs-lookup"><span data-stu-id="fc170-115">This cmdlet returns a list of all software packages that have been installed using PackageManagement.</span></span>

```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## <a name="get-packageprovider-cmdletpowershellmodulepackagemanagementget-packageprovider"></a>[<span data-ttu-id="fc170-116">Командлет Get-PackageProvider</span><span class="sxs-lookup"><span data-stu-id="fc170-116">Get-PackageProvider Cmdlet</span></span>](/powershell/module/PackageManagement/Get-PackageProvider)

<span data-ttu-id="fc170-117">С помощью этого командлета можно выполнить инвентаризацию поставщиков пакетов, которые уже загружены и готовы к использованию на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fc170-117">Package providers that are loaded and ready to be used on the local machine can be inventoried by using the cmdlet.</span></span>

```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## <a name="get-packagesource-cmdletpowershellmodulepackagemanagementget-packagesource"></a>[<span data-ttu-id="fc170-118">Командлет Get-PackageSource</span><span class="sxs-lookup"><span data-stu-id="fc170-118">Get-PackageSource Cmdlet</span></span>](/powershell/module/PackageManagement/Get-PackageSource)

<span data-ttu-id="fc170-119">Этот командлет возвращает список источников пакетов, зарегистрированных для поставщика пакетов.</span><span class="sxs-lookup"><span data-stu-id="fc170-119">This cmdlet gets a list of package sources that are registered for a package provider.</span></span>

```powershell
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## <a name="import-packageprovider-cmdletpowershellmodulepackagemanagementimport-packageprovider"></a>[<span data-ttu-id="fc170-120">Командлет Import-PackageProvider</span><span class="sxs-lookup"><span data-stu-id="fc170-120">Import-PackageProvider Cmdlet</span></span>](/powershell/module/PackageManagement/Import-PackageProvider)

<span data-ttu-id="fc170-121">Этот командлет добавляет поставщиков пакетов для управления пакетами в текущий сеанс.</span><span class="sxs-lookup"><span data-stu-id="fc170-121">This cmdlet adds Package Management package providers to the current session.</span></span>

```powershell
# Import a package provider from the local machine
Import-PackageProvider –Name MyProvider

#The -Name parameter can be either the name of the provider or the full path to the provider. Currently, we support .dll, .exe and.psm1 for the full path case. If the name of the provider is used for the -Name parameter, then additional version parameters such as -RequiredVersion, -MinimumVersion and -MaximumVersion may be specified. Otherwise, the latest version of the provider will be imported.

#If a package provider is not yet loaded to your system, we can discover and install on-demand. You can use explicit discovery and install cmdlets to do so:
 Find-PackageProvider
 Install-PackageProvider –Name MyProvider

#After installed, follow the Import-PackageProvider to load it to your system.

# Import a specific version of a package provider. PackageManagement supports installations of multiple versions of a package provider using PackageProvider cmdlets (not by bootstrapper provider). You can install another version of a package provider given that you already have one up running by:
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force
Get-PackageProvider –ListAvailable
Import-PackageProvider –Name "Nuget" -RequiredVersion "2.8.5.201" -Verbose
Import-PackageProvider –Name MyProvider –RequiredVersion xxxx -force
```

## <a name="install-package-cmdletpowershellmodulepackagemanagementinstall-package"></a>[<span data-ttu-id="fc170-122">Командлет Install-Package</span><span class="sxs-lookup"><span data-stu-id="fc170-122">Install-Package Cmdlet</span></span>](/powershell/module/PackageManagement/Install-Package)

<span data-ttu-id="fc170-123">Этот командлет обеспечивает установку пакетов программного обеспечения в доступных источниках с помощью загруженных поставщиков пакетов.</span><span class="sxs-lookup"><span data-stu-id="fc170-123">This cmdlet allows installation of software packages in available package sources using loaded package providers.</span></span>

```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## <a name="install-packageprovider-cmdletpowershellmodulepackagemanagementinstall-packageprovider"></a>[<span data-ttu-id="fc170-124">Командлет Install-PackageProvider</span><span class="sxs-lookup"><span data-stu-id="fc170-124">Install-PackageProvider Cmdlet</span></span>](/powershell/module/PackageManagement/Install-PackageProvider)

<span data-ttu-id="fc170-125">Этот командлет устанавливает один или несколько поставщиков пакетов для управления пакетами.</span><span class="sxs-lookup"><span data-stu-id="fc170-125">This cmdlet installs one or more Package Management package providers.</span></span>

```powershell
# Install a package provider from the PowerShell Gallery
Install-PackageProvider –Name "Gistprovider" -Verbose

# Install a specified version of a package provider
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force

# Find a provider and install it
Find-PackageProvider –Name "Gistprovider" | Install-PackageProvider -Verbose

# Install a provider to the current user’s module folder
Install-PackageProvider –Name Gistprovider –Verbose –Scope CurrentUser
```

## <a name="register-packagesource-cmdletpowershellmodulepackagemanagementregister-packagesource"></a>[<span data-ttu-id="fc170-126">Командлет Register-PackageSource</span><span class="sxs-lookup"><span data-stu-id="fc170-126">Register-PackageSource Cmdlet</span></span>](/powershell/module/PackageManagement/Register-PackageSource)

<span data-ttu-id="fc170-127">Этот командлет добавляет источник пакетов для указанного поставщика пакетов.</span><span class="sxs-lookup"><span data-stu-id="fc170-127">This cmdlet adds a package source for a specified package provider.</span></span>
<span data-ttu-id="fc170-128">Каждый поставщик PackageManagement может иметь один или несколько источников программного обеспечения или репозиториев.</span><span class="sxs-lookup"><span data-stu-id="fc170-128">Each PackageManagement provider may have one or multiple software sources, or repositories.</span></span> <span data-ttu-id="fc170-129">PackageManagement предоставляет командлеты PowerShell для добавления, удаления и запроса источника.</span><span class="sxs-lookup"><span data-stu-id="fc170-129">PackageManagement provides PowerShell cmdlets to add/remove/query the source.</span></span> <span data-ttu-id="fc170-130">Например, можно зарегистрировать источник пакетов для поставщика NuGet:</span><span class="sxs-lookup"><span data-stu-id="fc170-130">For example, you can register a package source for the NuGet provider:</span></span>

```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## <a name="save-package-cmdletpowershellmodulepackagemanagementsave-package"></a>[<span data-ttu-id="fc170-131">Командлет Save-Package</span><span class="sxs-lookup"><span data-stu-id="fc170-131">Save-Package Cmdlet</span></span>](/powershell/module/PackageManagement/Save-Package)

<span data-ttu-id="fc170-132">Этот командлет сохраняет пакеты на локальном компьютере без установки.</span><span class="sxs-lookup"><span data-stu-id="fc170-132">This cmdlet saves packages to the local computer without installing them.</span></span>

```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -Source c:\test
```

## <a name="set-packagesource-cmdletpowershellmodulepackagemanagementset-packagesource"></a>[<span data-ttu-id="fc170-133">Командлет Set-PackageSource</span><span class="sxs-lookup"><span data-stu-id="fc170-133">Set-PackageSource Cmdlet</span></span>](/powershell/module/PackageManagement/Set-PackageSource)

<span data-ttu-id="fc170-134">Этот командлет изменяет сведения о существующем источнике пакетов.</span><span class="sxs-lookup"><span data-stu-id="fc170-134">This cmdlet changes information about an existing package source.</span></span>

```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2
```

## <a name="uninstall-package-cmdletpowershellmodulepackagemanagementuninstall-package"></a>[<span data-ttu-id="fc170-135">Командлет Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="fc170-135">Uninstall-Package Cmdlet</span></span>](/powershell/module/PackageManagement/Uninstall-Package)

<span data-ttu-id="fc170-136">Этот командлет удаляет пакеты, установленные на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fc170-136">This cmdlet uninstalls packages installed on the local computer.</span></span>

```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## <a name="unregister-packagesource-cmdletpowershellmodulepackagemanagementunregister-packagesource"></a>[<span data-ttu-id="fc170-137">Командлет Unregister-PackageSource</span><span class="sxs-lookup"><span data-stu-id="fc170-137">Unregister-PackageSource Cmdlet</span></span>](/powershell/module/PackageManagement/Unregister-PackageSource)

```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```