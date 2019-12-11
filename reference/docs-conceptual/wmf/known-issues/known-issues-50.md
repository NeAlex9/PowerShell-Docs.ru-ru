---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
title: Известные проблемы в WMF 5.0
ms.openlocfilehash: 91f556cb43ef971107f05c4041b725b1c7e4f1bd
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "71147744"
---
# <a name="known-issues-in-wmf-50"></a><span data-ttu-id="10cc5-103">Известные проблемы в WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="10cc5-103">Known Issues in WMF 5.0</span></span>

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="10cc5-104">PowerShell ярлыки перестают работать при первом использовании</span><span class="sxs-lookup"><span data-stu-id="10cc5-104">PowerShell Shortcuts are broken when used for the first time</span></span>

<span data-ttu-id="10cc5-105">**Решение** Выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="10cc5-105">**Resolution:** Perform one of the following actions:</span></span>

1. <span data-ttu-id="10cc5-106">Щелкните ярлык PowerShell правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="10cc5-106">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="10cc5-107">Выберите Windows PowerShell для запуска в режиме без повышенных прав.</span><span class="sxs-lookup"><span data-stu-id="10cc5-107">Select "Windows PowerShell" to launch in a non-elevated mode.</span></span>
2. <span data-ttu-id="10cc5-108">Щелкните ярлык PowerShell правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="10cc5-108">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="10cc5-109">Щелкните Windows PowerShell правой кнопкой мыши и выберите пункт "Запуск от имени администратора" для запуска в режиме с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="10cc5-109">Right click on "Windows PowerShell" and select "Run As Administrator" to launch in an elevated mode.</span></span>

<span data-ttu-id="10cc5-110">После выполнения любого из указанных действий ярлыки PowerShell будут работать.</span><span class="sxs-lookup"><span data-stu-id="10cc5-110">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="10cc5-111">Эти действия требуется выполнить всего один раз.</span><span class="sxs-lookup"><span data-stu-id="10cc5-111">These actions need to be performed only once.</span></span>

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="10cc5-112">Модули PowerShell и ресурсы DSC выдает ошибки для ExecutionPolicy в Windows 7</span><span class="sxs-lookup"><span data-stu-id="10cc5-112">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>

<span data-ttu-id="10cc5-113">В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.</span><span class="sxs-lookup"><span data-stu-id="10cc5-113">On Windows 7, using PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="10cc5-114">**Решение** Задайте для ExecutionPolicy значение **RemoteSigned**, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):</span><span class="sxs-lookup"><span data-stu-id="10cc5-114">**Resolution:** Set the ExecutionPolicy to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="10cc5-115">Подключение к старой удаленной конечной точки Exchange вызывает сбой</span><span class="sxs-lookup"><span data-stu-id="10cc5-115">Connecting to an old remote Exchange endpoint causes a crash</span></span>

<span data-ttu-id="10cc5-116">Старая конечная точка Exchange выполняет перенаправление на новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="10cc5-116">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="10cc5-117">В логике перенаправления имеется ошибка, которая вызывает сбой.</span><span class="sxs-lookup"><span data-stu-id="10cc5-117">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="10cc5-118">**Решение** Подключитесь непосредственно к новой конечной точке.</span><span class="sxs-lookup"><span data-stu-id="10cc5-118">**Resolution:** Connect directly to the new endpoint.</span></span>

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="10cc5-119">Функция инвентаризации программного обеспечения ошибочно остановлена после установки WMF 5.0 в Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="10cc5-119">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>

<span data-ttu-id="10cc5-120">При установке WMF 5.0 в Windows Server 2012 R2, где уже выполняется инвентаризации программного обеспечения, эта функция ошибочно останавливается после установки.</span><span class="sxs-lookup"><span data-stu-id="10cc5-120">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="10cc5-121">**Решение** Запустите командлет `Start-SilLogging` один раз после установки WMF, так как процесс его установки ошибочно останавливает функцию инвентаризации программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="10cc5-121">**Resolution:** Run the `Start-SilLogging` cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="10cc5-122">`Get-ChildItem` не работает, если -LiteralPath и -Recurse используются совместно</span><span class="sxs-lookup"><span data-stu-id="10cc5-122">`Get-ChildItem` does not work if -LiteralPath and -Recurse are used together</span></span>

<span data-ttu-id="10cc5-123">Если имя каталога содержит недопустимый подстановочный знак, то `Get-ChildItem` не дает ожидаемые результаты при совместном использовании -LiteralPath и -Recurse.</span><span class="sxs-lookup"><span data-stu-id="10cc5-123">If a directory name contains an invalid wildcard character, then `Get-ChildItem` will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="10cc5-124">**Решение** В настоящее время обходной путь, хотя он и не является оптимальным, заключается в реализации рекурсии в скрипте вместо использования командлета.</span><span class="sxs-lookup"><span data-stu-id="10cc5-124">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>

## <a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="10cc5-125">Sysprep не работает после установки WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="10cc5-125">Sysprep fails after WMF 5.0 installation</span></span>

<span data-ttu-id="10cc5-126">Существует два способа решения этой проблемы в зависимости от используемой версии Windows Server.</span><span class="sxs-lookup"><span data-stu-id="10cc5-126">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="10cc5-127">**Решение**</span><span class="sxs-lookup"><span data-stu-id="10cc5-127">**Resolution:**</span></span>

- <span data-ttu-id="10cc5-128">Для систем под управлением **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="10cc5-128">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="10cc5-129">Откройте PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="10cc5-129">Open PowerShell as an administrator</span></span>
  2. <span data-ttu-id="10cc5-130">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="10cc5-130">Run the following command</span></span>

     ```powershell
     Set-SilLogging -TargetUri https://BlankTarget -CertificateThumbprint 0123456789
     ```

  3. <span data-ttu-id="10cc5-131">Выполните команду и пропустите ошибку, так как она ожидалась.</span><span class="sxs-lookup"><span data-stu-id="10cc5-131">Run the command and ignore the error, as they are expected.</span></span>

     ```powershell
     Publish-SilData
     ```

  4. <span data-ttu-id="10cc5-132">Удалите файлы в каталоге \Windows\System32\Logfiles\SIL\.</span><span class="sxs-lookup"><span data-stu-id="10cc5-132">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. <span data-ttu-id="10cc5-133">Установите все доступные важные обновления Windows и запустите Sysyprep в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="10cc5-133">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>

- <span data-ttu-id="10cc5-134">Для систем под управлением **Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="10cc5-134">For systems running **Windows Server 2012**</span></span>
  1. <span data-ttu-id="10cc5-135">После установки WMF 5.0 на сервере, где предполагается выполнить Sysprep, войдите в систему как администратор.</span><span class="sxs-lookup"><span data-stu-id="10cc5-135">After installing WMF 5.0 on the server to be Sysprep'd, login as administrator.</span></span>
  2. <span data-ttu-id="10cc5-136">Скопируйте файл Generize.xml из каталога `\Windows\System32\Sysprep\ActionFiles\` в расположение за пределами каталога Windows, например `C:\`.</span><span class="sxs-lookup"><span data-stu-id="10cc5-136">Copy Generize.xml from directory `\Windows\System32\Sysprep\ActionFiles\` to a location outside of the Windows directory, `C:\` for example.</span></span>
  3. <span data-ttu-id="10cc5-137">Откройте копию Generalize.xml в блокноте.</span><span class="sxs-lookup"><span data-stu-id="10cc5-137">Open your Generalize.xml copy with notepad.</span></span>
  4. <span data-ttu-id="10cc5-138">Найдите и удалите следующий текст: нужно удалить по одному экземпляру каждой строки (они находятся ближе к концу документа).</span><span class="sxs-lookup"><span data-stu-id="10cc5-138">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. <span data-ttu-id="10cc5-139">Сохраните измененную копию Generalize.xml и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="10cc5-139">Save the edited copy of Generalize.xml and close the file.</span></span>
  6. <span data-ttu-id="10cc5-140">Откройте командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="10cc5-140">Open a command prompt as administrator</span></span>
  7. <span data-ttu-id="10cc5-141">Выполните следующую команду, чтобы стать владельцем файла Generalize.xml в папке system32:</span><span class="sxs-lookup"><span data-stu-id="10cc5-141">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. <span data-ttu-id="10cc5-142">Выполните следующую команду, чтобы установить соответствующее разрешение для доступа к файлу:</span><span class="sxs-lookup"><span data-stu-id="10cc5-142">Run the following command to set appropriate permission on the file:</span></span>

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - <span data-ttu-id="10cc5-143">Ответьте "Да" в запросе на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="10cc5-143">Answer Yes at the prompt for confirmation.</span></span>
     - <span data-ttu-id="10cc5-144">Обратите внимание, что `<AdministratorUserName>` следует заменить именем пользователя, который является администратором на данном компьютере.</span><span class="sxs-lookup"><span data-stu-id="10cc5-144">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="10cc5-145">Например, "Administrator".</span><span class="sxs-lookup"><span data-stu-id="10cc5-145">For example, "Administrator".</span></span>

  9. <span data-ttu-id="10cc5-146">Скопируйте измененный и сохраненный файл в каталог Sysprep, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="10cc5-146">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - <span data-ttu-id="10cc5-147">В запросе ответьте "Да", чтобы перезаписать файл (если запрос на перезапись не появится, перепроверьте введенный путь).</span><span class="sxs-lookup"><span data-stu-id="10cc5-147">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
     - <span data-ttu-id="10cc5-148">Предполагается, что измененная копия Generalize.xml скопирована в каталог C:\.</span><span class="sxs-lookup"><span data-stu-id="10cc5-148">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10. <span data-ttu-id="10cc5-149">Теперь файл Generalize.xml изменен.</span><span class="sxs-lookup"><span data-stu-id="10cc5-149">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="10cc5-150">Запустите программу Sysprep с включенным параметром generalize.</span><span class="sxs-lookup"><span data-stu-id="10cc5-150">Please run Sysprep with the generalize option enabled.</span></span>