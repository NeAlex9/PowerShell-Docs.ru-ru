---
external help file: PSModule-help.xml
Locale: en-US
Module Name: PowerShellGet
ms.date: 10/03/2019
online version: https://docs.microsoft.com/powershell/module/powershellget/publish-module?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Publish-Module
ms.openlocfilehash: 2edc05ff660cfcca232af878c593c29de68eb122
ms.sourcegitcommit: 22c93550c87af30c4895fcb9e9dd65e30d60ada0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/19/2020
ms.locfileid: "99604789"
---
# <span data-ttu-id="fa866-102">Publish-Module</span><span class="sxs-lookup"><span data-stu-id="fa866-102">Publish-Module</span></span>

## <span data-ttu-id="fa866-103">Краткий обзор</span><span class="sxs-lookup"><span data-stu-id="fa866-103">SYNOPSIS</span></span>
<span data-ttu-id="fa866-104">Публикует указанный модуль с локального компьютера в коллекцию в Интернете.</span><span class="sxs-lookup"><span data-stu-id="fa866-104">Publishes a specified module from the local computer to an online gallery.</span></span>

## <span data-ttu-id="fa866-105">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="fa866-105">SYNTAX</span></span>

### <span data-ttu-id="fa866-106">Модуленамепараметерсет (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="fa866-106">ModuleNameParameterSet (Default)</span></span>

```
Publish-Module -Name <String> [-RequiredVersion <String>] [-NuGetApiKey <String>]
 [-Repository <String>] [-Credential <PSCredential>] [-FormatVersion <Version>]
 [-ReleaseNotes <String[]>] [-Tags <String[]>] [-LicenseUri <Uri>] [-IconUri <Uri>]
 [-ProjectUri <Uri>] [-Exclude <String[]>] [-Force] [-AllowPrerelease] [-SkipAutomaticTags]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

### <span data-ttu-id="fa866-107">модулепаспараметерсет</span><span class="sxs-lookup"><span data-stu-id="fa866-107">ModulePathParameterSet</span></span>

```
Publish-Module -Path <String> [-NuGetApiKey <String>] [-Repository <String>]
 [-Credential <PSCredential>] [-FormatVersion <Version>] [-ReleaseNotes <String[]>]
 [-Tags <String[]>] [-LicenseUri <Uri>] [-IconUri <Uri>] [-ProjectUri <Uri>] [-Force]
 [-SkipAutomaticTags] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## <span data-ttu-id="fa866-108">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="fa866-108">DESCRIPTION</span></span>

<span data-ttu-id="fa866-109">`Publish-Module`Командлет публикует модуль в коллекции на основе NuGet через Интернет, используя ключ API, хранящийся как часть профиля пользователя в коллекции.</span><span class="sxs-lookup"><span data-stu-id="fa866-109">The `Publish-Module` cmdlet publishes a module to an online NuGet-based gallery by using an API key, stored as part of a user's profile in the gallery.</span></span> <span data-ttu-id="fa866-110">Модуль для публикации можно указывать с помощью имени модуля или пути к папке, содержащей модуль.</span><span class="sxs-lookup"><span data-stu-id="fa866-110">You can specify the module to publish either by the module's name, or by the path to the folder containing the module.</span></span>

<span data-ttu-id="fa866-111">При указании модуля по имени `Publish-Module` публикует первый модуль, который можно найти, выполнив `Get-Module -ListAvailable <Name>` .</span><span class="sxs-lookup"><span data-stu-id="fa866-111">When you specify a module by name, `Publish-Module` publishes the first module that would be found by running `Get-Module -ListAvailable <Name>`.</span></span> <span data-ttu-id="fa866-112">Если указана минимальная версия модуля для публикации, `Publish-Module` публикует первый модуль с версией, которая больше или равна указанной минимальной версии.</span><span class="sxs-lookup"><span data-stu-id="fa866-112">If you specify a minimum version of a module to publish, `Publish-Module` publishes the first module with a version that is greater than or equal to the minimum version that you have specified.</span></span>

<span data-ttu-id="fa866-113">Для публикации модуля требуются метаданные, которые отображаются на странице коллекции для этого модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-113">Publishing a module requires metadata that is displayed on the gallery page for the module.</span></span> <span data-ttu-id="fa866-114">Обязательные метаданные включают имя модуля, версию, описание и автора.</span><span class="sxs-lookup"><span data-stu-id="fa866-114">Required metadata includes the module name, version, description, and author.</span></span> <span data-ttu-id="fa866-115">Хотя большинство метаданных берутся из манифеста модуля, некоторые метаданные должны быть указаны в `Publish-Module` параметрах, таких как **Tag**, **релеасеноте**, **IconUri**, **ProjectUri** и **LicenseUri**, так как эти параметры соответствуют полям в коллекции на основе NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa866-115">Although most metadata is taken from the module manifest, some metadata must be specified in `Publish-Module` parameters, such as **Tag**, **ReleaseNote**, **IconUri**, **ProjectUri**, and **LicenseUri**, because these parameters match fields in a NuGet-based gallery.</span></span>

## <span data-ttu-id="fa866-116">Примеры</span><span class="sxs-lookup"><span data-stu-id="fa866-116">EXAMPLES</span></span>

### <span data-ttu-id="fa866-117">Пример 1. Публикация модуля</span><span class="sxs-lookup"><span data-stu-id="fa866-117">Example 1: Publish a module</span></span>

<span data-ttu-id="fa866-118">В этом примере Мидскмодуле публикуется в веб-коллекции с помощью ключа API для указания учетной записи коллекции в Интернете владельца модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-118">In this example, MyDscModule is published to the online gallery by using the API key to indicate the module owner's online gallery account.</span></span> <span data-ttu-id="fa866-119">Если Мидскмодуле не является допустимым модулем манифеста, который указывает имя, версию, описание и автора, возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="fa866-119">If MyDscModule is not a valid manifest module that specifies a name, version, description, and author, an error occurs.</span></span>

```powershell
Publish-Module -Name "MyDscModule" -NuGetApiKey "11e4b435-6cb4-4bf7-8611-5162ed75eb73"
```

### <span data-ttu-id="fa866-120">Пример 2. Публикация модуля с метаданными коллекции</span><span class="sxs-lookup"><span data-stu-id="fa866-120">Example 2: Publish a module with gallery metadata</span></span>

<span data-ttu-id="fa866-121">В этом примере Мидскмодуле публикуется в Интернет-коллекции с помощью ключа API для указания учетной записи коллекции владельца модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-121">In this example, MyDscModule is published to the online gallery by using the API key to indicate the module owner's gallery account.</span></span> <span data-ttu-id="fa866-122">Дополнительные метаданные отображаются на веб-странице модуля в коллекции.</span><span class="sxs-lookup"><span data-stu-id="fa866-122">The additional metadata provided is displayed on the webpage for the module in the gallery.</span></span> <span data-ttu-id="fa866-123">Владелец добавляет два тега поиска для модуля, соотнесенный с Active Directory; будет добавлена Краткая заметка о выпуске.</span><span class="sxs-lookup"><span data-stu-id="fa866-123">The owner adds two search tags for the module, relating it to Active Directory; a brief release note is added.</span></span> <span data-ttu-id="fa866-124">Если Мидскмодуле не является допустимым модулем манифеста, который указывает имя, версию, описание и автора, возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="fa866-124">If MyDscModule is not a valid manifest module that specifies a name, version, description, and author, an error occurs.</span></span>

```powershell
Publish-Module -Name "MyDscModule" -NuGetApiKey "11e4b435-6cb4-4bf7-8611-5162ed75eb73" -LicenseUri "http://contoso.com/license" -Tag "Active Directory","DSC" -ReleaseNote "Updated the ActiveDirectory DSC Resources to support adding users."
```

## <span data-ttu-id="fa866-125">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="fa866-125">PARAMETERS</span></span>

### <span data-ttu-id="fa866-126">-AllowPrerelease</span><span class="sxs-lookup"><span data-stu-id="fa866-126">-AllowPrerelease</span></span>

<span data-ttu-id="fa866-127">Разрешает публикацию модулей, помеченных как предварительные.</span><span class="sxs-lookup"><span data-stu-id="fa866-127">Allows modules marked as prerelease to be published.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ModuleNameParameterSet
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-128">-Confirm</span><span class="sxs-lookup"><span data-stu-id="fa866-128">-Confirm</span></span>

<span data-ttu-id="fa866-129">Запрашивает подтверждение перед запуском `Publish-Module` .</span><span class="sxs-lookup"><span data-stu-id="fa866-129">Prompts you for confirmation before running the `Publish-Module`.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-130">-Credential</span><span class="sxs-lookup"><span data-stu-id="fa866-130">-Credential</span></span>

<span data-ttu-id="fa866-131">Указывает учетную запись пользователя, имеющую права на публикацию модуля для указанного поставщика пакетов или источника.</span><span class="sxs-lookup"><span data-stu-id="fa866-131">Specifies a user account that has rights to publish a module for a specified package provider or source.</span></span>

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

### <span data-ttu-id="fa866-132">-Exclude</span><span class="sxs-lookup"><span data-stu-id="fa866-132">-Exclude</span></span>

<span data-ttu-id="fa866-133">Определяет файлы, исключаемые из опубликованного модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-133">Defines files to exclude from the published module.</span></span>

```yaml
Type: System.String[]
Parameter Sets: ModuleNameParameterSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-134">-Force</span><span class="sxs-lookup"><span data-stu-id="fa866-134">-Force</span></span>

<span data-ttu-id="fa866-135">Принудительное выполнение команды без запроса на подтверждение пользователем.</span><span class="sxs-lookup"><span data-stu-id="fa866-135">Forces the command to run without asking for user confirmation.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-136">-FormatVersion</span><span class="sxs-lookup"><span data-stu-id="fa866-136">-FormatVersion</span></span>

<span data-ttu-id="fa866-137">Принимает только допустимые значения, указанные в атрибуте **Validate** .</span><span class="sxs-lookup"><span data-stu-id="fa866-137">Accepts only valid values specified by the **ValidateSet** attribute.</span></span>

<span data-ttu-id="fa866-138">Дополнительные сведения см. в [статьях объявление атрибута](/powershell/scripting/developer/cmdlet/validateset-attribute-declaration) и [валидатесетаттрибуте](/dotnet/api/system.management.automation.validatesetattribute).</span><span class="sxs-lookup"><span data-stu-id="fa866-138">For more information, see [ValidateSet Attribute Declaration](/powershell/scripting/developer/cmdlet/validateset-attribute-declaration) and [ValidateSetAttribute](/dotnet/api/system.management.automation.validatesetattribute).</span></span>

```yaml
Type: System.Version
Parameter Sets: (All)
Aliases:
Accepted values: 2.0

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-139">-IconUri</span><span class="sxs-lookup"><span data-stu-id="fa866-139">-IconUri</span></span>

<span data-ttu-id="fa866-140">Задает URL-адрес значка для модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-140">Specifies the URL of an icon for the module.</span></span> <span data-ttu-id="fa866-141">Указанный значок отображается на веб-странице коллекции модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-141">The specified icon is displayed on the gallery webpage for the module.</span></span>

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-142">-LicenseUri</span><span class="sxs-lookup"><span data-stu-id="fa866-142">-LicenseUri</span></span>

<span data-ttu-id="fa866-143">Указывает URL-адрес условий лицензирования для модуля, который вы хотите опубликовать.</span><span class="sxs-lookup"><span data-stu-id="fa866-143">Specifies the URL of licensing terms for the module you want to publish.</span></span>

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-144">-Name</span><span class="sxs-lookup"><span data-stu-id="fa866-144">-Name</span></span>

<span data-ttu-id="fa866-145">Указывает имя модуля, который необходимо опубликовать.</span><span class="sxs-lookup"><span data-stu-id="fa866-145">Specifies the name of the module that you want to publish.</span></span> <span data-ttu-id="fa866-146">`Publish-Module` выполняет поиск указанного имени модуля в `$Env:PSModulePath` .</span><span class="sxs-lookup"><span data-stu-id="fa866-146">`Publish-Module` searches for the specified module name in `$Env:PSModulePath`.</span></span>

```yaml
Type: System.String
Parameter Sets: ModuleNameParameterSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-147">-NuGetApiKey</span><span class="sxs-lookup"><span data-stu-id="fa866-147">-NuGetApiKey</span></span>

<span data-ttu-id="fa866-148">Указывает ключ API, который вы хотите использовать для публикации модуля в интерактивной коллекции.</span><span class="sxs-lookup"><span data-stu-id="fa866-148">Specifies the API key that you want to use to publish a module to the online gallery.</span></span> <span data-ttu-id="fa866-149">Ключ API является частью вашего профиля в интерактивной коллекции, и его можно найти на странице учетной записи пользователя в коллекции.</span><span class="sxs-lookup"><span data-stu-id="fa866-149">The API key is part of your profile in the online gallery, and can be found on your user account page in the gallery.</span></span> <span data-ttu-id="fa866-150">Ключ API — это специальные функции NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa866-150">The API key is NuGet-specific functionality.</span></span>

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

### <span data-ttu-id="fa866-151">-Path</span><span class="sxs-lookup"><span data-stu-id="fa866-151">-Path</span></span>

<span data-ttu-id="fa866-152">Указывает путь к модулю, который необходимо опубликовать.</span><span class="sxs-lookup"><span data-stu-id="fa866-152">Specifies the path to the module that you want to publish.</span></span> <span data-ttu-id="fa866-153">Этот параметр принимает путь к папке, содержащей модуль.</span><span class="sxs-lookup"><span data-stu-id="fa866-153">This parameter accepts the path to the folder that contains the module.</span></span>

```yaml
Type: System.String
Parameter Sets: ModulePathParameterSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-154">-ProjectUri</span><span class="sxs-lookup"><span data-stu-id="fa866-154">-ProjectUri</span></span>

<span data-ttu-id="fa866-155">Указывает URL-адрес веб-страницы об этом проекте.</span><span class="sxs-lookup"><span data-stu-id="fa866-155">Specifies the URL of a webpage about this project.</span></span>

```yaml
Type: System.Uri
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-156">-ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa866-156">-ReleaseNotes</span></span>

<span data-ttu-id="fa866-157">Указывает строку, содержащую заметки о выпуске или комментарии, которые должны быть доступны пользователям данной версии модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-157">Specifies a string containing release notes or comments that you want to be available to users of this version of the module.</span></span>

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

### <span data-ttu-id="fa866-158">— Репозиторий;</span><span class="sxs-lookup"><span data-stu-id="fa866-158">-Repository</span></span>

<span data-ttu-id="fa866-159">Указывает понятное имя репозитория, зарегистрированного при выполнении `Register-PSRepository` .</span><span class="sxs-lookup"><span data-stu-id="fa866-159">Specifies the friendly name of a repository that has been registered by running `Register-PSRepository`.</span></span> <span data-ttu-id="fa866-160">Репозиторий должен иметь **публишлокатион**, который является допустимым URI NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa866-160">The repository must have a **PublishLocation**, which is a valid NuGet URI.</span></span>
<span data-ttu-id="fa866-161">**Публишлокатион** можно задать, выполнив `Set-PSRepository` .</span><span class="sxs-lookup"><span data-stu-id="fa866-161">The **PublishLocation** can be set by running `Set-PSRepository`.</span></span>

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

### <span data-ttu-id="fa866-162">-RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="fa866-162">-RequiredVersion</span></span>

<span data-ttu-id="fa866-163">Указывает точную версию одного модуля для публикации.</span><span class="sxs-lookup"><span data-stu-id="fa866-163">Specifies the exact version of a single module to publish.</span></span>

```yaml
Type: System.String
Parameter Sets: ModuleNameParameterSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-164">-Скипаутоматиктагс</span><span class="sxs-lookup"><span data-stu-id="fa866-164">-SkipAutomaticTags</span></span>

<span data-ttu-id="fa866-165">Удаляет команды и ресурсы из включения в качестве тегов.</span><span class="sxs-lookup"><span data-stu-id="fa866-165">Removes commands and resources from being included as tags.</span></span> <span data-ttu-id="fa866-166">Пропускает автоматическое добавление тегов в модуль.</span><span class="sxs-lookup"><span data-stu-id="fa866-166">Skips automatically adding tags to a module.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-167">-Теги</span><span class="sxs-lookup"><span data-stu-id="fa866-167">-Tags</span></span>

<span data-ttu-id="fa866-168">Добавляет один или несколько тегов в публикуемый модуль.</span><span class="sxs-lookup"><span data-stu-id="fa866-168">Adds one or more tags to the module that you are publishing.</span></span> <span data-ttu-id="fa866-169">Примеры тегов: Десиредстатеконфигуратион, DSC, Дскресаурцекит или PSModule.</span><span class="sxs-lookup"><span data-stu-id="fa866-169">Example tags include DesiredStateConfiguration, DSC, DSCResourceKit, or PSModule.</span></span> <span data-ttu-id="fa866-170">Несколько тегов разделяются запятыми.</span><span class="sxs-lookup"><span data-stu-id="fa866-170">Separate multiple tags with commas.</span></span>

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

### <span data-ttu-id="fa866-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="fa866-171">-WhatIf</span></span>

<span data-ttu-id="fa866-172">Показывает, что произойдет при `Publish-Module` выполнении.</span><span class="sxs-lookup"><span data-stu-id="fa866-172">Shows what would happen if the `Publish-Module` runs.</span></span> <span data-ttu-id="fa866-173">Командлет не выполняется.</span><span class="sxs-lookup"><span data-stu-id="fa866-173">The cmdlet is not run.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="fa866-174">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="fa866-174">CommonParameters</span></span>

<span data-ttu-id="fa866-175">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fa866-175">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="fa866-176">См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="fa866-176">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="fa866-177">Входные данные</span><span class="sxs-lookup"><span data-stu-id="fa866-177">INPUTS</span></span>

### <span data-ttu-id="fa866-178">System.String</span><span class="sxs-lookup"><span data-stu-id="fa866-178">System.String</span></span>

### <span data-ttu-id="fa866-179">System.Management.Automation.PSCredential</span><span class="sxs-lookup"><span data-stu-id="fa866-179">System.Management.Automation.PSCredential</span></span>

## <span data-ttu-id="fa866-180">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="fa866-180">OUTPUTS</span></span>

### <span data-ttu-id="fa866-181">System.Object</span><span class="sxs-lookup"><span data-stu-id="fa866-181">System.Object</span></span>

## <span data-ttu-id="fa866-182">ПРИМЕЧАНИЯ</span><span class="sxs-lookup"><span data-stu-id="fa866-182">NOTES</span></span>

<span data-ttu-id="fa866-183">`Publish-Module` работает в PowerShell 3,0 или более поздних версиях PowerShell, в Windows 7 или Windows 2008 R2 и более поздних версиях Windows.</span><span class="sxs-lookup"><span data-stu-id="fa866-183">`Publish-Module` runs on PowerShell 3.0 or later releases of PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa866-184">Начиная с апреля 2020 года коллекция PowerShell не поддерживает протокол TLS (Transport Layer Security) версий 1.0 и 1.1.</span><span class="sxs-lookup"><span data-stu-id="fa866-184">As of April 2020, the PowerShell Gallery no longer supports Transport Layer Security (TLS) versions 1.0 and 1.1.</span></span> <span data-ttu-id="fa866-185">Если вы не используете TLS 1.2 или более поздней версии, при попытке доступа к коллекции PowerShell возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="fa866-185">If you are not using TLS 1.2 or higher, you will receive an error when trying to access the PowerShell Gallery.</span></span> <span data-ttu-id="fa866-186">Чтобы проверить, используется ли TLS 1.2, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fa866-186">Use the following command to ensure you are using TLS 1.2:</span></span>
>
> `[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12`
>
> <span data-ttu-id="fa866-187">Дополнительные сведения см. в [объявлении](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) в блоге, посвященном PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa866-187">For more information, see the [announcement](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/) in the PowerShell blog.</span></span>

<span data-ttu-id="fa866-188">Для публикации модуля требуются метаданные, которые отображаются на странице коллекции для этого модуля.</span><span class="sxs-lookup"><span data-stu-id="fa866-188">Publishing a module requires metadata that is displayed on the gallery page for the module.</span></span> <span data-ttu-id="fa866-189">Обязательные метаданные включают имя модуля, версию, описание и автора.</span><span class="sxs-lookup"><span data-stu-id="fa866-189">Required metadata includes the module name, version, description, and author.</span></span> <span data-ttu-id="fa866-190">Большинство метаданных берутся из манифеста модуля, но некоторые метаданные могут быть указаны в `Publish-Module` параметрах, таких как **Tag**, **релеасеноте**, **IconUri**, **ProjectUri** и **LicenseUri**.</span><span class="sxs-lookup"><span data-stu-id="fa866-190">Most metadata is taken from the module manifest, but some metadata can be specified in `Publish-Module` parameters, such as **Tag**, **ReleaseNote**, **IconUri**, **ProjectUri**, and **LicenseUri**.</span></span> <span data-ttu-id="fa866-191">Дополнительные сведения см. [в разделе значения манифеста пакета, которые влияют на коллекция PowerShell пользовательский интерфейс](/powershell/scripting/gallery/concepts/package-manifest-affecting-ui).</span><span class="sxs-lookup"><span data-stu-id="fa866-191">For more information, see [Package manifest values that impact the PowerShell Gallery UI](/powershell/scripting/gallery/concepts/package-manifest-affecting-ui).</span></span>

## <span data-ttu-id="fa866-192">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="fa866-192">RELATED LINKS</span></span>

[<span data-ttu-id="fa866-193">Find-Module</span><span class="sxs-lookup"><span data-stu-id="fa866-193">Find-Module</span></span>](Find-Module.md)

[<span data-ttu-id="fa866-194">Install-Module</span><span class="sxs-lookup"><span data-stu-id="fa866-194">Install-Module</span></span>](Install-Module.md)

[<span data-ttu-id="fa866-195">Register-PSRepository</span><span class="sxs-lookup"><span data-stu-id="fa866-195">Register-PSRepository</span></span>](Register-PSRepository.md)

[<span data-ttu-id="fa866-196">Set-PSRepository</span><span class="sxs-lookup"><span data-stu-id="fa866-196">Set-PSRepository</span></span>](Set-PSRepository.md)

[<span data-ttu-id="fa866-197">Uninstall-Module</span><span class="sxs-lookup"><span data-stu-id="fa866-197">Uninstall-Module</span></span>](Uninstall-Module.md)

[<span data-ttu-id="fa866-198">Update-Module</span><span class="sxs-lookup"><span data-stu-id="fa866-198">Update-Module</span></span>](Update-Module.md)
