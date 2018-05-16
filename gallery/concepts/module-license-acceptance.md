---
ms.date: 06/09/2017
schema: 2.0.0
keywords: powershell
title: Модули, для использования которых требуется принять условия лицензии
ms.openlocfilehash: fe197ea271e18580a221ad4d5245b685bd81775b
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="modules-requiring-license-acceptance"></a><span data-ttu-id="21237-103">Модули, для использования которых требуется принять условия лицензии</span><span class="sxs-lookup"><span data-stu-id="21237-103">Modules Requiring License Acceptance</span></span>

## <a name="synopsis"></a><span data-ttu-id="21237-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="21237-104">SYNOPSIS</span></span>

<span data-ttu-id="21237-105">В юридических требованиях некоторых издателей модулей указано, что перед установкой модуля из коллекции PowerShell пользователи должны явным образом принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-105">Legal departments for some module publishers require that customers must explicitly accept the license before installing their module from PowerShell Gallery.</span></span> <span data-ttu-id="21237-106">Если пользователь устанавливает, обновляет или сохраняет такой модуль с помощью PowerShellGet (непосредственно или как зависимость для другого элемента), он должен указать, что принимает такие условия. Иначе операция завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="21237-106">If a user installs, updates, or saves a module using PowerShellGet, whether directly or as a dependency for another item, and that module requires the user to agree to a license, the user must indicate they accept the license or the operation fails.</span></span>

## <a name="publish-requirements-for-modules"></a><span data-ttu-id="21237-107">Требования к публикации модулей</span><span class="sxs-lookup"><span data-stu-id="21237-107">Publish Requirements for Modules</span></span>

<span data-ttu-id="21237-108">Модули, для использования которых нужно принять условия лицензионного соглашения, должны соответствовать следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="21237-108">Modules that would like to require users to accept license should fulfill following requirements:</span></span>

- <span data-ttu-id="21237-109">В разделе PSData манифеста модуля для параметра RequireLicenseAcceptance должно быть установлено значение $True.</span><span class="sxs-lookup"><span data-stu-id="21237-109">PSData section of module manifest should include RequireLicenseAcceptance = $True.</span></span>
- <span data-ttu-id="21237-110">В корневом каталоге модуля должен содержаться файл license.txt.</span><span class="sxs-lookup"><span data-stu-id="21237-110">Module should contain license.txt file in root directory.</span></span>
- <span data-ttu-id="21237-111">Манифест модуля должен содержать URI лицензии.</span><span class="sxs-lookup"><span data-stu-id="21237-111">Module manifest should contain License Uri.</span></span>
- <span data-ttu-id="21237-112">Модуль должен быть опубликован в формате PowerShellGet 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="21237-112">Module should be published with PowerShellGet Format Version 2.0 and above.</span></span>

## <a name="impact-on-installsaveupdate-module"></a><span data-ttu-id="21237-113">Влияние на командлеты Install/Save/Update-Module</span><span class="sxs-lookup"><span data-stu-id="21237-113">Impact on Install/Save/Update-Module</span></span>

- <span data-ttu-id="21237-114">Командлеты установки, сохранения и обновления будут поддерживать новый параметр -AcceptLicense. Его поведение аналогично действиям пользователя после прочтения лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-114">Install/Save/Update cmdlets will support a new parameter –AcceptLicense that will behave as though the user saw the license.</span></span>
- <span data-ttu-id="21237-115">Если для параметра RequiredLicenseAcceptance установлено значение True, а параметр -AcceptLicense не указан, для пользователя будет отображаться файл license.txt и запрос &quot;Вы принимаете условия лицензионного соглашения? (Yes/No/YesToAll/NoToAll)&quot;.</span><span class="sxs-lookup"><span data-stu-id="21237-115">If RequiredLicenseAcceptance is True and –AcceptLicense is not specified, the user will be shown the license.txt, and prompted with: &quot;Do you accept these license terms (Yes/No/YesToAll/NoToAll)&quot;.</span></span>
  - <span data-ttu-id="21237-116">Если условия лицензионного соглашения принимаются:</span><span class="sxs-lookup"><span data-stu-id="21237-116">If the license is accepted</span></span>
    - <span data-ttu-id="21237-117">**Save-Module:** модуль будет скопирован в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="21237-117">**Save-Module:** the module will be copied to the user&#39;s system</span></span>
    - <span data-ttu-id="21237-118">**Install-Module:** модуль будет скопирован в надлежащую папку в системе пользователя (в зависимости от области действия).</span><span class="sxs-lookup"><span data-stu-id="21237-118">**Install-Module:** the module will be copied to the user&#39;s system to the proper folder (based on scope)</span></span>
    - <span data-ttu-id="21237-119">**Update-Module:** модуль будет обновлен.</span><span class="sxs-lookup"><span data-stu-id="21237-119">**Update-Module:** the module will be updated.</span></span>
  - <span data-ttu-id="21237-120">Если условия лицензионного соглашения отклоняются:</span><span class="sxs-lookup"><span data-stu-id="21237-120">If the license is declined.</span></span>
    - <span data-ttu-id="21237-121">Операция будет отменена.</span><span class="sxs-lookup"><span data-stu-id="21237-121">Operation will be cancelled.</span></span>
- <span data-ttu-id="21237-122">Все командлеты проверяют метаданные (requireLicenseAcceptance и версию формата), которые свидетельствуют о том, что требуется принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-122">All cmdlets will check for the metadata(requireLicenseAcceptance and Format Version) that says a license acceptance is required</span></span>
  - <span data-ttu-id="21237-123">Если версия формата клиента ниже 2.0, операция завершится ошибкой. Поступит запрос на обновление клиента.</span><span class="sxs-lookup"><span data-stu-id="21237-123">If format version of client is older than 2.0, operation will fail and ask the user to update the client.</span></span>
  - <span data-ttu-id="21237-124">Если модуль опубликован с версией формата ниже 2.0, флаг requireLicenseAcceptance будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="21237-124">If module was published with format version older than 2.0, requireLicenseAcceptance flag will be ignored.</span></span>


 ## <a name="module-dependencies"></a><span data-ttu-id="21237-125">Зависимости модулей</span><span class="sxs-lookup"><span data-stu-id="21237-125">Module Dependencies</span></span>
- <span data-ttu-id="21237-126">Если при установке, сохранении или обновлении зависимого модуля (или модуля, от которого зависят другие функции) требуется принять условия лицензионного соглашения, примите их (процедура описана выше).</span><span class="sxs-lookup"><span data-stu-id="21237-126">During Install/Save/Update operation, if a dependent module(something else depends on the module) requires license acceptance, then the license acceptance behavior (above) will be required.</span></span>
- <span data-ttu-id="21237-127">Если версия модуля уже указана в локальном каталоге как установленная в системе, пропустите процедуру проверки лицензии.</span><span class="sxs-lookup"><span data-stu-id="21237-127">If the module version is already listed in the local catalog as being installed on the system, we would bypass the license checking.</span></span>
- <span data-ttu-id="21237-128">Если при установке, сохранении или обновлении зависимого модуля требуется принять условия лицензионного соглашения, но они не принимаются, операция завершится ошибкой. Будут выполняться стандартные процессы, сопровождающие ошибку установки, сохранения или обновления элемента.</span><span class="sxs-lookup"><span data-stu-id="21237-128">During Install/Save/Update operation, if a dependent module requires a license, and the license acceptance does not occur, the operation will fail and follow normal processes for the item failed to install/save/update.</span></span>

 ## <a name="impact-on--force"></a><span data-ttu-id="21237-129">Влияние на параметр -Force</span><span class="sxs-lookup"><span data-stu-id="21237-129">Impact on -Force</span></span>

<span data-ttu-id="21237-130">Указание -Force НЕ является достаточным для принятия условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-130">Specifying –Force is NOT sufficient to accept a license.</span></span> <span data-ttu-id="21237-131">Для разрешения на установку требуется указать -AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="21237-131">–AcceptLicense is required for permission to install.</span></span> <span data-ttu-id="21237-132">Если указан параметр -Force, RequiredLicenseAcceptance имеет значение True, а параметр -AcceptLicense НЕ указан, операция завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="21237-132">If –Force is specified, RequiredLicenseAcceptance is True, and –AcceptLicense is NOT specified, the operation will fail.</span></span>

## <a name="examples"></a><span data-ttu-id="21237-133">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="21237-133">EXAMPLES</span></span>

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a><span data-ttu-id="21237-134">Пример 1. Обновление манифеста модуля для запроса на принятие условий лицензионного соглашения</span><span class="sxs-lookup"><span data-stu-id="21237-134">Example 1: Update Module Manifest to require license acceptance</span></span>

```PowerShell
PS> Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance

PrivateData = @{

    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

<span data-ttu-id="21237-135">Эта команда позволяет обновить файл манифеста и установить для флага RequireLicenseAcceptance значение true.</span><span class="sxs-lookup"><span data-stu-id="21237-135">This command updates the manifest file and sets the RequireLicenseAcceptance flag to true.</span></span>

### <a name="example-2-install-module-requiring-license-acceptance"></a><span data-ttu-id="21237-136">Пример 2. Установка модуля, для использования которого требуется принять условия лицензионного соглашения</span><span class="sxs-lookup"><span data-stu-id="21237-136">Example 2: Install Module requiring license acceptance</span></span>

```PowerShell
PS> Install-Module -Name ModuleRequireLicenseAcceptance

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):

```

<span data-ttu-id="21237-137">Эта команда предназначена для отображения лицензии в файле license.txt и запроса на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-137">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="21237-138">Пример 3. Установка модуля, для использования которого требуется принять условия лицензионного соглашения, при помощи -AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="21237-138">Example 3: Install Module requiring license acceptance with -AcceptLicense</span></span>

```PowerShell
PS> Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

<span data-ttu-id="21237-139">Модуль устанавливается без запросов на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-139">Module is installed without any prompt to accept license.</span></span>

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a><span data-ttu-id="21237-140">Пример 4. Установка модуля, для использования которого требуется принять условия лицензионного соглашения при помощи -Force</span><span class="sxs-lookup"><span data-stu-id="21237-140">Example 4: Install Module requiring license acceptance with -Force</span></span>

```PowerShell
PS> Install-Module -Name ModuleRequireLicenseAcceptance -Force
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="21237-141">Пример 5. Установка модуля с зависимостями, для использования которого требуется принять условия лицензионного соглашения</span><span class="sxs-lookup"><span data-stu-id="21237-141">Example 5: Install Module with dependencies requiring license acceptance</span></span>

<span data-ttu-id="21237-142">Модуль ModuleWithDependency зависит от модуля ModuleRequireLicenseAcceptance.</span><span class="sxs-lookup"><span data-stu-id="21237-142">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="21237-143">Пользователю предлагается принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-143">User is prompted to Accept License.</span></span>

```PowerShell
PS> Install-Module -Name ModuleWithDependency

License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="21237-144">Пример 6. Установка модуля с зависимостями, для использования которого требуется принять условия лицензионного соглашения и указать -AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="21237-144">Example 6: Install Module with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="21237-145">Модуль ModuleWithDependency зависит от модуля ModuleRequireLicenseAcceptance.</span><span class="sxs-lookup"><span data-stu-id="21237-145">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="21237-146">Пользователю не предлагается принять условия лицензии, так как указан параметр -AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="21237-146">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```PowerShell
PS>  Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a><span data-ttu-id="21237-147">Пример 7. Установка модуля, для использования которого требуется принять условия лицензионного соглашения, в клиенте с версией ниже, чем PSGetFormatVersion 2.0</span><span class="sxs-lookup"><span data-stu-id="21237-147">Example 7: Install module requiring license acceptance on a client older than PSGetFormatVersion 2.0</span></span>

```PowerShell
PS C:\windows\system32> Install-Module -Name ModuleRequireLicenseAcceptance

WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.

```

### <a name="example-8-save-module-requiring-license-acceptance"></a><span data-ttu-id="21237-148">Пример 8. Сохранение модуля, для использования которого требуется принять условия лицензионного соглашения</span><span class="sxs-lookup"><span data-stu-id="21237-148">Example 8: Save Module requiring license acceptance</span></span>

```PowerShell
PS> Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="21237-149">Эта команда предназначена для отображения лицензии в файле license.txt и запроса на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-149">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="21237-150">Пример 9. Сохранение модуля, для использования которого требуется принять условия лицензионного соглашения, при помощи -AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="21237-150">Example 9: Save Module requiring license acceptance with -AcceptLicense</span></span>

```PowerShell
PS> Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

<span data-ttu-id="21237-151">Модуль сохраняется без запроса на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-151">Module is saved without any prompt to accept license.</span></span>

### <a name="example-10-update-module-requiring-license-acceptance"></a><span data-ttu-id="21237-152">Пример 10. Обновление модуля, для использования которого требуется принять условия лицензионного соглашения</span><span class="sxs-lookup"><span data-stu-id="21237-152">Example 10: Update Module requiring license acceptance</span></span>

```PowerShell
PS> Update-Module -Name ModuleRequireLicenseAcceptance

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="21237-153">Эта команда предназначена для отображения лицензии в файле license.txt и запроса на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-153">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="21237-154">Пример 11. Обновление модуля, для использования которого требуется принять условия лицензионного соглашения, при помощи -AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="21237-154">Example 11: Update Module requiring license acceptance with -AcceptLicense</span></span>

```PowerShell
PS> Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

<span data-ttu-id="21237-155">Модуль обновляется без запроса на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="21237-155">Module is updated without any prompt to accept license.</span></span>

## <a name="more-details"></a><span data-ttu-id="21237-156">Дополнительные подробности</span><span class="sxs-lookup"><span data-stu-id="21237-156">More details</span></span>

### <a name="require-license-acceptance-for-scriptsscript-license-acceptancemd"></a>[<span data-ttu-id="21237-157">Запрос на принятие условий лицензии для скриптов</span><span class="sxs-lookup"><span data-stu-id="21237-157">Require License Acceptance for Scripts</span></span>](./script-license-acceptance.md)

### <a name="require-license-acceptance-support-on-powershellgalleryhow-toworking-with-itemsitems-that-require-license-acceptancemd"></a>[<span data-ttu-id="21237-158">Поддержка запроса на принятие условий лицензионного соглашения в коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="21237-158">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-items/items-that-require-license-acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationhow-toworking-with-itemsdeploy-to-azure-automationmd"></a>[<span data-ttu-id="21237-159">Запрос на принятие условий лицензии при развертывании в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="21237-159">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-items/deploy-to-azure-automation.md)