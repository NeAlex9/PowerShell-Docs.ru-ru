---
description: Переменная среды PSModulePath содержит список расположений папок, в которых выполняется поиск модулей и ресурсов.
Locale: en-US
ms.date: 11/11/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_PSModulePath?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_PSModulePath
ms.openlocfilehash: ce77005d816f49c0a6353bd7b3e0580293b05d23
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "99601485"
---
# <a name="about-psmodulepath"></a><span data-ttu-id="57eb2-103">О PSModulePath</span><span class="sxs-lookup"><span data-stu-id="57eb2-103">About PSModulePath</span></span>

<span data-ttu-id="57eb2-104">`$env:PSModulePath`Переменная среды содержит список расположений папок, в которых выполняется поиск модулей и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="57eb2-104">The `$env:PSModulePath` environment variable contains a list of folder locations that are searched to find modules and resources.</span></span> <span data-ttu-id="57eb2-105">PowerShell рекурсивно ищет в каждой папке файлы модулей ( `.psd1` или `.psm1` ).</span><span class="sxs-lookup"><span data-stu-id="57eb2-105">PowerShell recursively searches each folder for module (`.psd1` or `.psm1`) files.</span></span>

<span data-ttu-id="57eb2-106">По умолчанию действующие расположения, назначенные, `$env:PSModulePath` являются:</span><span class="sxs-lookup"><span data-stu-id="57eb2-106">By default, the effective locations assigned to `$env:PSModulePath` are:</span></span>

- <span data-ttu-id="57eb2-107">Расположения на уровне системы. Эти папки содержат модули, поставляемые с PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-107">System-wide locations: These folders contain modules that ship with PowerShell.</span></span> <span data-ttu-id="57eb2-108">Эти модули хранятся в `$PSHOME\Modules` папке.</span><span class="sxs-lookup"><span data-stu-id="57eb2-108">These modules are store in the `$PSHOME\Modules` folder.</span></span> <span data-ttu-id="57eb2-109">Это также расположение, в котором установлены модули управления Windows.</span><span class="sxs-lookup"><span data-stu-id="57eb2-109">This is also the location where the Windows management modules are installed.</span></span>

- <span data-ttu-id="57eb2-110">Модули, установленные пользователем: это модули, установленные пользователем.</span><span class="sxs-lookup"><span data-stu-id="57eb2-110">User-installed modules: These are modules installed by the user.</span></span>
  <span data-ttu-id="57eb2-111">`Install-Module` имеет параметр **области** , который позволяет указать, установлен ли модуль для текущего пользователя или для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="57eb2-111">`Install-Module` has a **Scope** parameter that allows you to specify whether the module is installed for the current user or for all users.</span></span> <span data-ttu-id="57eb2-112">Дополнительные сведения см. в разделе [Install-Module](xref:PowerShellGet.Install-Module).</span><span class="sxs-lookup"><span data-stu-id="57eb2-112">For more information, see [Install-Module](xref:PowerShellGet.Install-Module).</span></span>

  - <span data-ttu-id="57eb2-113">В Windows расположением определяемой пользователем области **CurrentUser** является `$HOME\Documents\PowerShell\Modules` Папка.</span><span class="sxs-lookup"><span data-stu-id="57eb2-113">On Windows, the location of the user-specific **CurrentUser** scope is the `$HOME\Documents\PowerShell\Modules` folder.</span></span> <span data-ttu-id="57eb2-114">Областью **ALLUSERS** является расположение `$env:ProgramFiles\PowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-114">The location of the **AllUsers** scope is `$env:ProgramFiles\PowerShell\Modules`.</span></span>
  - <span data-ttu-id="57eb2-115">В системах, отличных от Windows, расположением определяемой пользователем области **CurrentUser** является `$HOME/.local/share/powershell/Modules` Папка.</span><span class="sxs-lookup"><span data-stu-id="57eb2-115">On non-Windows systems, the location of the user-specific **CurrentUser** scope is the `$HOME/.local/share/powershell/Modules` folder.</span></span> <span data-ttu-id="57eb2-116">Областью **ALLUSERS** является расположение `/usr/local/share/powershell/Modules` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-116">The location of the **AllUsers** scope is `/usr/local/share/powershell/Modules`.</span></span>

<span data-ttu-id="57eb2-117">Кроме того, программы установки, устанавливающие модули в других каталогах, например каталог Program Files, могут добавлять свои расположения к значению `$env:PSModulePath` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-117">In addition, setup programs that install modules in other directories, such as the Program Files directory, can append their locations to the value of `$env:PSModulePath`.</span></span>

> [!NOTE]
> <span data-ttu-id="57eb2-118">В Windows пользовательское расположение — это `PowerShell\Modules` Папка, расположенная в папке **документы** в профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="57eb2-118">On Windows, the user-specific location is the `PowerShell\Modules` folder located in the **Documents** folder in your user profile.</span></span> <span data-ttu-id="57eb2-119">Конкретный путь к этому расположению зависит от версии Windows, а также от того, используется ли перенаправление папок.</span><span class="sxs-lookup"><span data-stu-id="57eb2-119">The specific path of that location varies by version of Windows and whether or not you are using folder redirection.</span></span> <span data-ttu-id="57eb2-120">Microsoft OneDrive также может изменить расположение папки **документов** .</span><span class="sxs-lookup"><span data-stu-id="57eb2-120">Microsoft OneDrive can also change the location of your **Documents** folder.</span></span> <span data-ttu-id="57eb2-121">Расположение папки **документов** можно проверить с помощью следующей команды: `[Environment]::GetFolderPath('MyDocuments')` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-121">You can verify the location of your **Documents** folder using the following command: `[Environment]::GetFolderPath('MyDocuments')`.</span></span>

## <a name="modifying-psmodulepath"></a><span data-ttu-id="57eb2-122">Изменение PSModulePath</span><span class="sxs-lookup"><span data-stu-id="57eb2-122">Modifying PSModulePath</span></span>

<span data-ttu-id="57eb2-123">Чтобы изменить каталоги модулей по умолчанию для текущего сеанса, используйте следующий формат команды, чтобы изменить значение `PSModulePath` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="57eb2-123">To change the default module directories for the current session, use the following command format to change the value of the `PSModulePath` environment variable.</span></span>

<span data-ttu-id="57eb2-124">Например, чтобы добавить `C:\Program Files\Fabrikam\Modules` Каталог к значению переменной среды PSModulePath, введите:</span><span class="sxs-lookup"><span data-stu-id="57eb2-124">For example, to add the `C:\Program Files\Fabrikam\Modules` directory to the value of the PSModulePath environment variable, type:</span></span>

```powershell
$Env:PSModulePath = $Env:PSModulePath+";C:\Program Files\Fabrikam\Modules"
```

<span data-ttu-id="57eb2-125">Точка с запятой ( `;` ) в команде отделяет новый путь от пути, расположенного перед ним в списке.</span><span class="sxs-lookup"><span data-stu-id="57eb2-125">The semi-colon (`;`) in the command separates the new path from the path that precedes it in the list.</span></span> <span data-ttu-id="57eb2-126">На платформах, отличных от Windows, двоеточие ( `:` ) разделяет расположения путей в переменной среды.</span><span class="sxs-lookup"><span data-stu-id="57eb2-126">On non-Windows platforms, the colon (`:`) separates the path locations in the environment variable.</span></span>

<span data-ttu-id="57eb2-127">Чтобы изменить значение `PSModulePath` в каждом сеансе, добавьте предыдущую команду в профиль PowerShell или используйте метод **SetEnvironmentVariable** класса **Environment** .</span><span class="sxs-lookup"><span data-stu-id="57eb2-127">To change the value of `PSModulePath` in every session, add the previous command to your PowerShell profile or use the **SetEnvironmentVariable** method of the **Environment** class.</span></span>

<span data-ttu-id="57eb2-128">Следующая команда использует метод **GetEnvironmentVariable** для получения параметра компьютера, `PSModulePath` а метод **SetEnvironmentVariable** — для добавления `C:\Program Files\Fabrikam\Modules` пути к значению.</span><span class="sxs-lookup"><span data-stu-id="57eb2-128">The following command uses the **GetEnvironmentVariable** method to get the machine setting of `PSModulePath` and the **SetEnvironmentVariable** method to add the `C:\Program Files\Fabrikam\Modules` path to the value.</span></span>

```powershell
$path = [Environment]::GetEnvironmentVariable('PSModulePath', 'Machine')
$newpath = $path + ';C:\Program Files\Fabrikam\Modules'
[Environment]::SetEnvironmentVariable('PSModulePath', $newpath, 'Machine')
```

<span data-ttu-id="57eb2-129">Чтобы добавить путь к пользовательскому параметру, измените целевое значение на " **пользователь**".</span><span class="sxs-lookup"><span data-stu-id="57eb2-129">To add a path to the user setting, change the target value to **User**.</span></span>

```powershell
$path = [Environment]::GetEnvironmentVariable('PSModulePath', 'User')
$newpath = $path + ';C:\Program Files\Fabrikam\Modules'
[Environment]::SetEnvironmentVariable('PSModulePath', $newpath, 'User')
```

<span data-ttu-id="57eb2-130">Дополнительные сведения о методах класса **System. Environment** см. в разделе [методы среды](/dotnet/api/system.environment).</span><span class="sxs-lookup"><span data-stu-id="57eb2-130">For more information about the methods of the **System.Environment** class, see [Environment Methods](/dotnet/api/system.environment).</span></span>

## <a name="powershell-psmodulepath-construction"></a><span data-ttu-id="57eb2-131">Создание PSModulePath PowerShell</span><span class="sxs-lookup"><span data-stu-id="57eb2-131">PowerShell PSModulePath construction</span></span>

<span data-ttu-id="57eb2-132">Значение формируется `$env:PSModulePath` каждый раз при запуске PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-132">The value of `$env:PSModulePath` is constructed each time PowerShell starts.</span></span>
<span data-ttu-id="57eb2-133">Значение зависит от версии PowerShell и способа ее запуска.</span><span class="sxs-lookup"><span data-stu-id="57eb2-133">The value varies by version of PowerShell and how it is launched.</span></span>

### <a name="windows-powershell-startup"></a><span data-ttu-id="57eb2-134">Запуск Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="57eb2-134">Windows PowerShell startup</span></span>

<span data-ttu-id="57eb2-135">Windows PowerShell использует следующую логику для создания `PSModulePath` при запуске.</span><span class="sxs-lookup"><span data-stu-id="57eb2-135">Windows PowerShell uses the following logic to construct the `PSModulePath` at startup:</span></span>

- <span data-ttu-id="57eb2-136">Если `PSModulePath` не существует, объедините пути **CurrentUser**, **ALLUSERS** и `$PSHOME` modules.</span><span class="sxs-lookup"><span data-stu-id="57eb2-136">If `PSModulePath` doesn't exist, combine **CurrentUser**, **AllUsers**, and the `$PSHOME` modules paths</span></span>
- <span data-ttu-id="57eb2-137">Если `PSModulePath` существует:</span><span class="sxs-lookup"><span data-stu-id="57eb2-137">If `PSModulePath` does exist:</span></span>
  - <span data-ttu-id="57eb2-138">Если `PSModulePath` содержит `$PSHOME` путь к модулям:</span><span class="sxs-lookup"><span data-stu-id="57eb2-138">If `PSModulePath` contains `$PSHOME` modules path:</span></span>
    - <span data-ttu-id="57eb2-139">Путь к модулям **ALLUSERS** вставляется перед `$PSHOME` путем к модулям</span><span class="sxs-lookup"><span data-stu-id="57eb2-139">**AllUsers** modules path is inserted before `$PSHOME` modules path</span></span>
  - <span data-ttu-id="57eb2-140">Кроме</span><span class="sxs-lookup"><span data-stu-id="57eb2-140">else:</span></span>
    - <span data-ttu-id="57eb2-141">Просто используйте `PSModulePath` , как определено, так как пользователь намеренно удалил `$PSHOME` расположение.</span><span class="sxs-lookup"><span data-stu-id="57eb2-141">Just use `PSModulePath` as defined since the user deliberately removed the `$PSHOME` location</span></span>

<span data-ttu-id="57eb2-142">Путь к модулю **CurrentUser** имеет префикс, только если область пользователя `$env:PSModulePath` не существует.</span><span class="sxs-lookup"><span data-stu-id="57eb2-142">The **CurrentUser** module path is prefixed only if User scope `$env:PSModulePath` doesn't exist.</span></span> <span data-ttu-id="57eb2-143">В противном случае область пользователя `$env:PSModulePath` будет использоваться как определенная.</span><span class="sxs-lookup"><span data-stu-id="57eb2-143">Otherwise, the User scope `$env:PSModulePath` is used as defined.</span></span>

### <a name="powershell-core-6-startup"></a><span data-ttu-id="57eb2-144">Запуск PowerShell Core 6</span><span class="sxs-lookup"><span data-stu-id="57eb2-144">PowerShell Core 6 startup</span></span>

<span data-ttu-id="57eb2-145">PowerShell Core 6 не использует содержимое, `$env:PSModulePath` если обнаруживает, что оно было запущено из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-145">PowerShell Core 6 doesn't use contents of `$env:PSModulePath` if it detects it was started from PowerShell.</span></span> <span data-ttu-id="57eb2-146">Он перезаписывает его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="57eb2-146">It overwrites it with:</span></span>

- <span data-ttu-id="57eb2-147">Модули **CurrentUser** путь + **ALLUSERS** модули путь + `$PSHOME` модули путь + `$PSHOME` путь к модулям Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-147">**CurrentUser** modules path + **AllUsers** modules path + `$PSHOME` modules path + Windows PowerShell `$PSHOME` modules path.</span></span>

### <a name="powershell-7-startup"></a><span data-ttu-id="57eb2-148">Запуск PowerShell 7</span><span class="sxs-lookup"><span data-stu-id="57eb2-148">PowerShell 7 startup</span></span>

<span data-ttu-id="57eb2-149">В Windows для большинства переменных среды, если переменная уровня пользователя существует, новый процесс использует это значение только в том случае, если переменная уровня компьютера с таким же именем существует.</span><span class="sxs-lookup"><span data-stu-id="57eb2-149">In Windows, for most environment variables, if the User-scoped variable exists, a new process uses that value only even if a Machine-scoped variable of the same name exists.</span></span>

<span data-ttu-id="57eb2-150">В PowerShell 7 `PSModulePath` обрабатывается аналогично тому, как `Path` переменная среды обрабатывается в Windows.</span><span class="sxs-lookup"><span data-stu-id="57eb2-150">In PowerShell 7, `PSModulePath` is treated similar to how the `Path` environment variable is treated on Windows.</span></span> <span data-ttu-id="57eb2-151">В Windows обрабатывается иначе, чем `Path` в других переменных среды.</span><span class="sxs-lookup"><span data-stu-id="57eb2-151">On Windows, `Path` is treated differently from other environment variables.</span></span> <span data-ttu-id="57eb2-152">При запуске процесса Windows объединяет область пользователя `Path` с областью действия компьютера `Path` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-152">When a process is started, Windows combines the User-scoped `Path` with the Machine-scoped `Path`.</span></span>

- <span data-ttu-id="57eb2-153">Получение области пользователя `PSModulePath`</span><span class="sxs-lookup"><span data-stu-id="57eb2-153">Retrieve the User-scoped `PSModulePath`</span></span>
- <span data-ttu-id="57eb2-154">Сравнить с наследуемой `PSModulePath` переменной среды</span><span class="sxs-lookup"><span data-stu-id="57eb2-154">Compare to process inherited `PSModulePath` environment variable</span></span>
  - <span data-ttu-id="57eb2-155">Если это так:</span><span class="sxs-lookup"><span data-stu-id="57eb2-155">If the same:</span></span>
    - <span data-ttu-id="57eb2-156">Добавьте **ALLUSERS** `PSModulePath` в конец, следующий за семантикой `Path` переменной среды</span><span class="sxs-lookup"><span data-stu-id="57eb2-156">Append the **AllUsers** `PSModulePath` to the end following the semantics of the `Path` environment variable</span></span>
    - <span data-ttu-id="57eb2-157">Путь Windows `System32` берется из определенного компьютера, `PSModulePath` поэтому его не нужно добавлять явно.</span><span class="sxs-lookup"><span data-stu-id="57eb2-157">The Windows `System32` path comes from the machine defined `PSModulePath` so does not need to be added explicitly</span></span>
  - <span data-ttu-id="57eb2-158">Если они отличаются, то следует рассматривать, как будто пользователь явно изменил его и не добавил **ALLUSERS**`PSModulePath`</span><span class="sxs-lookup"><span data-stu-id="57eb2-158">If different, treat as though user explicitly modified it and don't append **AllUsers** `PSModulePath`</span></span>
- <span data-ttu-id="57eb2-159">Префикс с PS7 пользователя, системой и `$PSHOME` путями в этом порядке</span><span class="sxs-lookup"><span data-stu-id="57eb2-159">Prefix with PS7 User, System, and `$PSHOME` paths in that order</span></span>
  - <span data-ttu-id="57eb2-160">Если параметр `powershell.config.json` содержит пользовательскую область `PSModulePath` , используйте его вместо значения по умолчанию для пользователя.</span><span class="sxs-lookup"><span data-stu-id="57eb2-160">If `powershell.config.json` contains a user scoped `PSModulePath`, use that instead of the default for the user</span></span>
  - <span data-ttu-id="57eb2-161">Если `powershell.config.json` содержит область системы `PSModulePath` , используйте ее вместо значения по умолчанию для системы</span><span class="sxs-lookup"><span data-stu-id="57eb2-161">If `powershell.config.json` contains a system scoped `PSModulePath`, use that instead of the default for the system</span></span>

<span data-ttu-id="57eb2-162">В системах UNIX не существует разделения переменных среды пользователя и системы.</span><span class="sxs-lookup"><span data-stu-id="57eb2-162">Unix systems don't have a separation of User and System environment variables.</span></span>
<span data-ttu-id="57eb2-163">`PSModulePath` является унаследованным, а пути, зависящие от PS7, являются префиксами, если они еще не определены.</span><span class="sxs-lookup"><span data-stu-id="57eb2-163">`PSModulePath` is inherited and the PS7-specific paths are prefixed if not already defined.</span></span>

### <a name="starting-windows-powershell-from-powershell-7"></a><span data-ttu-id="57eb2-164">Запуск Windows PowerShell из PowerShell 7</span><span class="sxs-lookup"><span data-stu-id="57eb2-164">Starting Windows PowerShell from PowerShell 7</span></span>

<span data-ttu-id="57eb2-165">В этом обсуждении _Windows PowerShell_ означает `powershell.exe` и, и `powershell_ise.exe` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-165">For this discussion, _Windows PowerShell_ means both `powershell.exe` and `powershell_ise.exe`.</span></span>

<span data-ttu-id="57eb2-166">Значение `$env:PSModulePath` копируется в `WinPSModulePath` со следующими изменениями:</span><span class="sxs-lookup"><span data-stu-id="57eb2-166">The value of `$env:PSModulePath` is copied to `WinPSModulePath` with the following modifications:</span></span>

- <span data-ttu-id="57eb2-167">Удалить PS7 путь к пользовательскому модулю</span><span class="sxs-lookup"><span data-stu-id="57eb2-167">Remove PS7 the User module path</span></span>
- <span data-ttu-id="57eb2-168">Удалить PS7 путь к системному модулю</span><span class="sxs-lookup"><span data-stu-id="57eb2-168">Remove PS7 the System module path</span></span>
- <span data-ttu-id="57eb2-169">Удалить PS7 в `$PSHOME` пути к модулю</span><span class="sxs-lookup"><span data-stu-id="57eb2-169">Remove PS7 the `$PSHOME` module path</span></span>

<span data-ttu-id="57eb2-170">Пути PS7 удаляются, чтобы модули PS7 не загружались в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-170">The PS7 paths are removed so that PS7 modules don't get loaded in Windows PowerShell.</span></span> <span data-ttu-id="57eb2-171">`WinPSModulePath`Значение используется при запуске Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-171">The `WinPSModulePath` value is used when starting Windows PowerShell.</span></span>

### <a name="starting-powershell-7-from-windows-powershell"></a><span data-ttu-id="57eb2-172">Запуск PowerShell 7 из Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="57eb2-172">Starting PowerShell 7 from Windows PowerShell</span></span>

<span data-ttu-id="57eb2-173">Запуск PowerShell 7 продолжится "как есть" с добавлением путей наследования, добавленных Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57eb2-173">The PowerShell 7 startup continues as-is with the addition of inheriting paths that Windows PowerShell added.</span></span> <span data-ttu-id="57eb2-174">Так как пути, относящиеся к PS7, являются префиксами, функциональные проблемы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="57eb2-174">Since the PS7-specific paths are prefixed, there is no functional issue.</span></span>

### <a name="starting-powershell-6-from-powershell-7"></a><span data-ttu-id="57eb2-175">Запуск PowerShell 6 из PowerShell 7</span><span class="sxs-lookup"><span data-stu-id="57eb2-175">Starting PowerShell 6 from PowerShell 7</span></span>

<span data-ttu-id="57eb2-176">PowerShell Core 6 перезаписывает `$env:PSModulePath` .</span><span class="sxs-lookup"><span data-stu-id="57eb2-176">PowerShell Core 6 overwrites `$env:PSModulePath`.</span></span> <span data-ttu-id="57eb2-177">Изменения не вносятся.</span><span class="sxs-lookup"><span data-stu-id="57eb2-177">No changes are made.</span></span>

### <a name="starting-powershell-7-from-powershell-6"></a><span data-ttu-id="57eb2-178">Запуск PowerShell 7 из PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="57eb2-178">Starting PowerShell 7 from PowerShell 6</span></span>

<span data-ttu-id="57eb2-179">Запуск PowerShell 7 продолжится как есть с добавлением путей, добавленных PowerShell Core 6.</span><span class="sxs-lookup"><span data-stu-id="57eb2-179">The PowerShell 7 startup continues as-is with the addition of inheriting paths that PowerShell Core 6 added.</span></span> <span data-ttu-id="57eb2-180">Так как пути, относящиеся к PS7, являются префиксами, функциональные проблемы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="57eb2-180">Since the PS7-specific paths are prefixed, there is no functional issue.</span></span>

## <a name="module-search-behavior"></a><span data-ttu-id="57eb2-181">Поведение поиска модулей</span><span class="sxs-lookup"><span data-stu-id="57eb2-181">Module search behavior</span></span>

<span data-ttu-id="57eb2-182">PowerShell рекурсивно ищет каждую папку в **PSModulePath** для файлов модуля ( `.psd1` или `.psm1` ).</span><span class="sxs-lookup"><span data-stu-id="57eb2-182">PowerShell recursively searches each folder in the **PSModulePath** for module (`.psd1` or `.psm1`) files.</span></span> <span data-ttu-id="57eb2-183">Этот шаблон поиска позволяет устанавливать несколько версий одного модуля в разных папках.</span><span class="sxs-lookup"><span data-stu-id="57eb2-183">This search pattern allows multiple versions of the same module to be installed in different folders.</span></span> <span data-ttu-id="57eb2-184">Пример:</span><span class="sxs-lookup"><span data-stu-id="57eb2-184">For example:</span></span>

```Output
    Directory: C:\Program Files\WindowsPowerShell\Modules\PowerShellGet

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----           8/14/2020  5:56 PM                1.0.0.1
d----           9/13/2019  3:53 PM                2.1.2
```

<span data-ttu-id="57eb2-185">По умолчанию PowerShell загружает самый высокий номер версии модуля при обнаружении нескольких версий.</span><span class="sxs-lookup"><span data-stu-id="57eb2-185">By default, PowerShell loads the highest version number of a module when multiple versions are found.</span></span> <span data-ttu-id="57eb2-186">Чтобы загрузить определенную версию, используйте `Import-Module` с параметром **FullyQualifiedName** .</span><span class="sxs-lookup"><span data-stu-id="57eb2-186">To load a specific version, use `Import-Module` with the **FullyQualifiedName** parameter.</span></span> <span data-ttu-id="57eb2-187">Дополнительные сведения см. в разделе [Import-Module](xref:Microsoft.PowerShell.Core.Import-Module).</span><span class="sxs-lookup"><span data-stu-id="57eb2-187">For more information, see [Import-Module](xref:Microsoft.PowerShell.Core.Import-Module).</span></span>

## <a name="see-also"></a><span data-ttu-id="57eb2-188">См. также</span><span class="sxs-lookup"><span data-stu-id="57eb2-188">See also</span></span>

- [<span data-ttu-id="57eb2-189">about_Modules</span><span class="sxs-lookup"><span data-stu-id="57eb2-189">about_Modules</span></span>](about_Modules.md)
- [<span data-ttu-id="57eb2-190">Методы среды</span><span class="sxs-lookup"><span data-stu-id="57eb2-190">Environment Methods</span></span>](/dotnet/api/system.environment)