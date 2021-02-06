---
description: Описывает, как подписывать сценарии, чтобы они соответствовали политикам выполнения PowerShell.
Locale: en-US
ms.date: 07/31/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_signing?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Signing
ms.openlocfilehash: 560ecc385e970224a23af7a1195c99d8423f503f
ms.sourcegitcommit: 021ea294327dec542ec040619dac0d2171397a90
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "99600201"
---
# <a name="about-signing"></a><span data-ttu-id="ef57a-103">О подписывании</span><span class="sxs-lookup"><span data-stu-id="ef57a-103">About Signing</span></span>

## <a name="short-description"></a><span data-ttu-id="ef57a-104">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="ef57a-104">Short description</span></span>
<span data-ttu-id="ef57a-105">Описывает, как подписывать сценарии, чтобы они соответствовали политикам выполнения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef57a-105">Explains how to sign scripts so that they comply with the PowerShell execution policies.</span></span>

## <a name="long-description"></a><span data-ttu-id="ef57a-106">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="ef57a-106">Long description</span></span>

<span data-ttu-id="ef57a-107">Политика ограниченного выполнения не позволяет запускать скрипты.</span><span class="sxs-lookup"><span data-stu-id="ef57a-107">The Restricted execution policy does not permit any scripts to run.</span></span> <span data-ttu-id="ef57a-108">Политики выполнения **AllSigned** и **RemoteSigned** запрещают PowerShell выполнять сценарии, не имеющие цифровой подписи.</span><span class="sxs-lookup"><span data-stu-id="ef57a-108">The **AllSigned** and **RemoteSigned** execution policies prevent PowerShell from running scripts that do not have a digital signature.</span></span>

<span data-ttu-id="ef57a-109">В этом разделе объясняется, как выполнить выбранные сценарии, которые не подписаны, даже если политика выполнения **RemoteSigned** и как подписывать сценарии для собственного использования.</span><span class="sxs-lookup"><span data-stu-id="ef57a-109">This topic explains how to run selected scripts that are not signed, even while the execution policy is **RemoteSigned**, and how to sign scripts for your own use.</span></span>

<span data-ttu-id="ef57a-110">Дополнительные сведения о политиках выполнения PowerShell см. в разделе [about_Execution_Policies](about_Execution_Policies.md).</span><span class="sxs-lookup"><span data-stu-id="ef57a-110">For more information about PowerShell execution policies, see [about_Execution_Policies](about_Execution_Policies.md).</span></span>

## <a name="to-permit-signed-scripts-to-run"></a><span data-ttu-id="ef57a-111">Разрешение выполнения подписанных сценариев</span><span class="sxs-lookup"><span data-stu-id="ef57a-111">To permit signed scripts to run</span></span>

<span data-ttu-id="ef57a-112">При первом запуске PowerShell на компьютере, скорее всего, действует политика **ограниченного** выполнения (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ef57a-112">When you start PowerShell on a computer for the first time, the **Restricted** execution policy (the default) is likely to be in effect.</span></span>

<span data-ttu-id="ef57a-113">Политика с **ограниченным доступом** не позволяет запускать скрипты.</span><span class="sxs-lookup"><span data-stu-id="ef57a-113">The **Restricted** policy does not permit any scripts to run.</span></span>

<span data-ttu-id="ef57a-114">Чтобы найти действующую политику выполнения на компьютере, введите:</span><span class="sxs-lookup"><span data-stu-id="ef57a-114">To find the effective execution policy on your computer, type:</span></span>

```powershell
Get-ExecutionPolicy
```

<span data-ttu-id="ef57a-115">Чтобы запустить неподписанные скрипты, написанные на локальном компьютере и подписанные скрипты от других пользователей, запустите PowerShell с параметром Запуск от имени администратора, а затем используйте следующую команду, чтобы изменить политику выполнения на компьютере на **RemoteSigned**:</span><span class="sxs-lookup"><span data-stu-id="ef57a-115">To run unsigned scripts that you write on your local computer and signed scripts from other users, start PowerShell with the Run as Administrator option and then use the following command to change the execution policy on the computer to **RemoteSigned**:</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<span data-ttu-id="ef57a-116">Дополнительные сведения см. в разделе справки по `Set-ExecutionPolicy` командлету.</span><span class="sxs-lookup"><span data-stu-id="ef57a-116">For more information, see the help topic for the `Set-ExecutionPolicy` cmdlet.</span></span>

## <a name="running-unsigned-scripts-using-the-remotesigned-execution-policy"></a><span data-ttu-id="ef57a-117">Выполнение неподписанных скриптов с помощью политики выполнения RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="ef57a-117">Running unsigned scripts using the RemoteSigned execution policy</span></span>

<span data-ttu-id="ef57a-118">Если политика выполнения PowerShell — **RemoteSigned**, PowerShell не будет запускать неподписанные сценарии, которые будут скачаны из Интернета, в том числе неподписанные сценарии, получаемые через электронную почту и программы обмена мгновенными сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ef57a-118">If your PowerShell execution policy is **RemoteSigned**, PowerShell will not run unsigned scripts that are downloaded from the internet, including unsigned scripts you receive through email and instant messaging programs.</span></span>

<span data-ttu-id="ef57a-119">При попытке запустить скачанный скрипт PowerShell выводит следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="ef57a-119">If you try to run a downloaded script, PowerShell displays the following error message:</span></span>

```Output
The file <file-name> cannot be loaded. The file <file-name> is not digitally
signed. The script will not execute on the system. Please see "Get-Help
about_Signing" for more details.
```

<span data-ttu-id="ef57a-120">Перед выполнением скрипта проверьте код, чтобы убедиться, что он является доверенным.</span><span class="sxs-lookup"><span data-stu-id="ef57a-120">Before you run the script, review the code to be sure that you trust it.</span></span>
<span data-ttu-id="ef57a-121">Сценарии имеют тот же результат, что и любая исполняемая программа.</span><span class="sxs-lookup"><span data-stu-id="ef57a-121">Scripts have the same effect as any executable program.</span></span>

<span data-ttu-id="ef57a-122">Чтобы выполнить неподписанный скрипт, используйте командлет Unblock-File или выполните следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="ef57a-122">To run an unsigned script, use the Unblock-File cmdlet or use the following procedure.</span></span>

1. <span data-ttu-id="ef57a-123">Сохраните файл скрипта на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ef57a-123">Save the script file on your computer.</span></span>
2. <span data-ttu-id="ef57a-124">Нажмите кнопку Пуск, выберите пункт Мой компьютер и перейдите к сохраненному файлу скрипта.</span><span class="sxs-lookup"><span data-stu-id="ef57a-124">Click Start, click My Computer, and locate the saved script file.</span></span>
3. <span data-ttu-id="ef57a-125">Щелкните правой кнопкой мыши файл скрипта и выберите пункт Свойства.</span><span class="sxs-lookup"><span data-stu-id="ef57a-125">Right-click the script file, and then click Properties.</span></span>
4. <span data-ttu-id="ef57a-126">Нажмите кнопку Снять блокировку.</span><span class="sxs-lookup"><span data-stu-id="ef57a-126">Click Unblock.</span></span>

<span data-ttu-id="ef57a-127">Если сценарий, скачанный из Интернета, имеет цифровую подпись, но вы еще не выбрали доверие к издателю, PowerShell выводит следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="ef57a-127">If a script that was downloaded from the internet is digitally signed, but you have not yet chosen to trust its publisher, PowerShell displays the following message:</span></span>

```Output
Do you want to run software from this untrusted publisher?
The file <file-name> is published by CN=<publisher-name>. This
publisher is not trusted on your system. Only run scripts
from trusted publishers.

[V] Never run  [D] Do not run  [R] Run once  [A] Always run
[?] Help (default is "D"):
```

<span data-ttu-id="ef57a-128">Если вы доверяете издателю, выберите "запустить один раз" или "всегда запускать".</span><span class="sxs-lookup"><span data-stu-id="ef57a-128">If you trust the publisher, select "Run once" or "Always run."</span></span> <span data-ttu-id="ef57a-129">Если вы не доверяете издателю, выберите параметр "никогда не запускать" или "не запускать".</span><span class="sxs-lookup"><span data-stu-id="ef57a-129">If you do not trust the publisher, select either "Never run" or "Do not run."</span></span> <span data-ttu-id="ef57a-130">Если выбрать параметр "никогда не запускать" или "всегда запускать", PowerShell не будет выводить запрос для этого издателя снова.</span><span class="sxs-lookup"><span data-stu-id="ef57a-130">If you select "Never run" or "Always run," PowerShell will not prompt you again for this publisher.</span></span>

## <a name="methods-of-signing-scripts"></a><span data-ttu-id="ef57a-131">Методы подписания скриптов</span><span class="sxs-lookup"><span data-stu-id="ef57a-131">Methods of signing scripts</span></span>

<span data-ttu-id="ef57a-132">Вы можете подписывать скрипты, которые вы пишете, и скрипты, получаемые из других источников.</span><span class="sxs-lookup"><span data-stu-id="ef57a-132">You can sign the scripts that you write and the scripts that you obtain from other sources.</span></span> <span data-ttu-id="ef57a-133">Перед тем как подписать любой сценарий, проверьте каждую команду, чтобы убедиться в том, что он является надежным для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ef57a-133">Before you sign any script, examine each command to verify that it is safe to run.</span></span>

<span data-ttu-id="ef57a-134">Рекомендации по подписывания кода см. в статье рекомендации по [подписывания](/previous-versions/windows/hardware/design/dn653556(v=vs.85))кода.</span><span class="sxs-lookup"><span data-stu-id="ef57a-134">For best practices about code signing, see [Code-Signing Best Practices](/previous-versions/windows/hardware/design/dn653556(v=vs.85)).</span></span>

<span data-ttu-id="ef57a-135">Дополнительные сведения о том, как подписать файл скрипта, см. в разделе [Set-AuthenticodeSignature](xref:Microsoft.PowerShell.Security.Set-AuthenticodeSignature).</span><span class="sxs-lookup"><span data-stu-id="ef57a-135">For more information about how to sign a script file, see [Set-AuthenticodeSignature](xref:Microsoft.PowerShell.Security.Set-AuthenticodeSignature).</span></span>

<span data-ttu-id="ef57a-136">`New-SelfSignedCertificate`Командлет, представленный в модуле PKI в PowerShell 3,0, создает самозаверяющий сертификат, подходящий для тестирования.</span><span class="sxs-lookup"><span data-stu-id="ef57a-136">The `New-SelfSignedCertificate` cmdlet, introduced in the PKI module in PowerShell 3.0, creates a self-signed certificate that is Appropriate for testing.</span></span> <span data-ttu-id="ef57a-137">Дополнительные сведения см. в разделе справки по командлету New-SelfSignedCertificate.</span><span class="sxs-lookup"><span data-stu-id="ef57a-137">For more information, see the help topic for the New-SelfSignedCertificate cmdlet.</span></span>

<span data-ttu-id="ef57a-138">Чтобы добавить цифровую подпись в скрипт, необходимо подписать его с помощью сертификата подписи кода.</span><span class="sxs-lookup"><span data-stu-id="ef57a-138">To add a digital signature to a script, you must sign it with a code signing certificate.</span></span> <span data-ttu-id="ef57a-139">Для подписи файла скрипта подходят два типа сертификатов:</span><span class="sxs-lookup"><span data-stu-id="ef57a-139">Two types of certificates are suitable for signing a script file:</span></span>

- <span data-ttu-id="ef57a-140">Сертификаты, созданные центром сертификации. для платной платы общедоступный центр сертификации проверяет ваше удостоверение и предоставляет сертификат подписи кода.</span><span class="sxs-lookup"><span data-stu-id="ef57a-140">Certificates that are created by a certification authority: For a fee, a public certification authority verifies your identity and gives you a code signing certificate.</span></span> <span data-ttu-id="ef57a-141">При приобретении сертификата от известного центра сертификации можно предоставить общий доступ к сценарию пользователям на других компьютерах под управлением Windows, так как эти компьютеры доверяют центру сертификации.</span><span class="sxs-lookup"><span data-stu-id="ef57a-141">When you purchase your certificate from a reputable certification authority, you are able to share your script with users on other computers that are running Windows because those other computers trust the certification authority.</span></span>

- <span data-ttu-id="ef57a-142">Создаваемые сертификаты: можно создать самозаверяющий сертификат, для которого компьютер является центром сертификации, который создает сертификат.</span><span class="sxs-lookup"><span data-stu-id="ef57a-142">Certificates that you create: You can create a self-signed certificate for which your computer is the authority that creates the certificate.</span></span> <span data-ttu-id="ef57a-143">Этот сертификат предоставляется бесплатно и позволяет писать, подписывать и выполнять сценарии на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ef57a-143">This certificate is free of charge and enables you to write, sign, and run scripts on your computer.</span></span> <span data-ttu-id="ef57a-144">Однако сценарий, подписанный самозаверяющим сертификатом, не будет выполняться на других компьютерах.</span><span class="sxs-lookup"><span data-stu-id="ef57a-144">However, a script signed by a self-signed certificate will not run on other computers.</span></span>

<span data-ttu-id="ef57a-145">Как правило, самозаверяющий сертификат используется только для подписывания сценариев, написанных для собственного использования, и для подписывания сценариев, получаемых из других источников, которые были проверены как надежные.</span><span class="sxs-lookup"><span data-stu-id="ef57a-145">Typically, you would use a self-signed certificate only to sign scripts that you write for your own use and to sign scripts that you get from other sources that you have verified to be safe.</span></span> <span data-ttu-id="ef57a-146">Он не подходит для сценариев, которые будут совместно использоваться даже в рамках предприятия.</span><span class="sxs-lookup"><span data-stu-id="ef57a-146">It is not appropriate for scripts that will be shared, even within an enterprise.</span></span>

<span data-ttu-id="ef57a-147">При создании самозаверяющего сертификата обязательно включите усиленную защиту закрытого ключа в сертификате.</span><span class="sxs-lookup"><span data-stu-id="ef57a-147">If you create a self-signed certificate, be sure to enable strong private key protection on your certificate.</span></span> <span data-ttu-id="ef57a-148">Это не позволит вредоносным программам подписывать сценарии от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="ef57a-148">This prevents malicious programs from signing scripts on your behalf.</span></span> <span data-ttu-id="ef57a-149">Инструкции включены в конце этого раздела.</span><span class="sxs-lookup"><span data-stu-id="ef57a-149">The instructions are included at the end of this topic.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ef57a-150">Создание самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="ef57a-150">Create a self-signed certificate</span></span>

<span data-ttu-id="ef57a-151">Чтобы создать самозаверяющий сертификат, используйте `New-SelfSignedCertificate` командлет в модуле PKI.</span><span class="sxs-lookup"><span data-stu-id="ef57a-151">To create a self-signed certificate, use the `New-SelfSignedCertificate` cmdlet in the PKI module.</span></span> <span data-ttu-id="ef57a-152">Этот модуль появился в PowerShell 3,0 и входит в Windows 8 и Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="ef57a-152">This module is introduced in PowerShell 3.0 and is included in Windows 8 and Windows Server 2012.</span></span> <span data-ttu-id="ef57a-153">Дополнительные сведения см. в разделе справки по `New-SelfSignedCertificate` командлету.</span><span class="sxs-lookup"><span data-stu-id="ef57a-153">For more information, see the help topic for the `New-SelfSignedCertificate` cmdlet.</span></span>

<span data-ttu-id="ef57a-154">Чтобы создать самозаверяющий сертификат в более ранних версиях Windows, используйте средство создания сертификатов `MakeCert.exe` .</span><span class="sxs-lookup"><span data-stu-id="ef57a-154">To create a self-signed certificate in earlier versions of Windows, use the Certificate Creation tool `MakeCert.exe`.</span></span> <span data-ttu-id="ef57a-155">Это средство входит в состав пакета SDK для Microsoft .NET (версии 1,1 и более поздних) и в Microsoft Windows SDK.</span><span class="sxs-lookup"><span data-stu-id="ef57a-155">This tool is included in the Microsoft .NET SDK (versions 1.1 and later) and in the Microsoft Windows SDK.</span></span>

<span data-ttu-id="ef57a-156">Дополнительные сведения о синтаксисе и описания параметров средства MakeCert.exe см. в разделе [средство создания сертификатов (MakeCert.exe)](/previous-versions/dotnet/netframework-2.0/bfsktky3(v=vs.80)).</span><span class="sxs-lookup"><span data-stu-id="ef57a-156">For more information about the syntax and the parameter descriptions of the MakeCert.exe tool, see [Certificate Creation Tool (MakeCert.exe)](/previous-versions/dotnet/netframework-2.0/bfsktky3(v=vs.80)).</span></span>

<span data-ttu-id="ef57a-157">Чтобы использовать средство MakeCert.exe для создания сертификата, выполните следующие команды в окне командной строки пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="ef57a-157">To use the MakeCert.exe tool to create a certificate, run the following commands in an SDK Command Prompt window.</span></span>

<span data-ttu-id="ef57a-158">Примечание. Первая команда создает локальный центр сертификации для компьютера.</span><span class="sxs-lookup"><span data-stu-id="ef57a-158">Note: The first command creates a local certification authority for your computer.</span></span> <span data-ttu-id="ef57a-159">Вторая команда создает личный сертификат из центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="ef57a-159">The second command generates a personal certificate from the certification authority.</span></span>

<span data-ttu-id="ef57a-160">Примечание. Вы можете скопировать или ввести команды в том виде, в каком они отображаются.</span><span class="sxs-lookup"><span data-stu-id="ef57a-160">Note: You can copy or type the commands exactly as they appear.</span></span> <span data-ttu-id="ef57a-161">Подстановки не требуются, хотя имя сертификата можно изменить.</span><span class="sxs-lookup"><span data-stu-id="ef57a-161">No substitutions are necessary, although you can change the certificate name.</span></span>

```powershell
makecert -n "CN=PowerShell Local Certificate Root" -a sha1 `
-eku 1.3.6.1.5.5.7.3.3 -r -sv root.pvk root.cer `
-ss Root -sr localMachine

makecert -pe -n "CN=PowerShell User" -ss MY -a sha1 `
-eku 1.3.6.1.5.5.7.3.3 -iv root.pvk -ic root.cer
```

<span data-ttu-id="ef57a-162">Средство MakeCert.exe предложит ввести пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="ef57a-162">The MakeCert.exe tool will prompt you for a private key password.</span></span> <span data-ttu-id="ef57a-163">Пароль гарантирует, что никто не сможет использовать сертификат или получить к нему доступ без вашего согласия.</span><span class="sxs-lookup"><span data-stu-id="ef57a-163">The password ensures that no one can use or access the certificate without your consent.</span></span>
<span data-ttu-id="ef57a-164">Создайте и введите пароль, который вы можете запомнить.</span><span class="sxs-lookup"><span data-stu-id="ef57a-164">Create and enter a password that you can remember.</span></span> <span data-ttu-id="ef57a-165">Этот пароль будет использоваться позже для получения сертификата.</span><span class="sxs-lookup"><span data-stu-id="ef57a-165">You will use this password later to retrieve the certificate.</span></span>

<span data-ttu-id="ef57a-166">Чтобы убедиться, что сертификат создан правильно, выполните следующую команду, чтобы получить сертификат в хранилище сертификатов на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ef57a-166">To verify that the certificate was generated correctly, use the following command to get the certificate in the certificate store on the computer.</span></span> <span data-ttu-id="ef57a-167">Файл сертификата не будет найден в каталоге файловой системы.</span><span class="sxs-lookup"><span data-stu-id="ef57a-167">You will not find a certificate file in the file system directory.</span></span>

<span data-ttu-id="ef57a-168">В командной строке PowerShell введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef57a-168">At the PowerShell prompt, type:</span></span>

```powershell
Get-ChildItem cert:\CurrentUser\my -codesigning
```

<span data-ttu-id="ef57a-169">Эта команда использует поставщик сертификата PowerShell для просмотра сведений о сертификате.</span><span class="sxs-lookup"><span data-stu-id="ef57a-169">This command uses the PowerShell Certificate provider to view information about the certificate.</span></span>

<span data-ttu-id="ef57a-170">Если сертификат создан, в выходных данных отображается **отпечаток** , который определяет сертификат в дисплее, похожем на следующий:</span><span class="sxs-lookup"><span data-stu-id="ef57a-170">If the certificate was created, the output shows the **thumbprint** that identifies the certificate in a display that resembles the following:</span></span>

```Output
Directory: Microsoft.PowerShell.Security\Certificate::CurrentUser\My

Thumbprint                                Subject
----------                                -------
4D4917CB140714BA5B81B96E0B18AAF2C4564FDF  CN=PowerShell User ]
```

## <a name="sign-a-script"></a><span data-ttu-id="ef57a-171">Подписать сценарий</span><span class="sxs-lookup"><span data-stu-id="ef57a-171">Sign a script</span></span>

<span data-ttu-id="ef57a-172">После создания самозаверяющего сертификата можно подписывать сценарии.</span><span class="sxs-lookup"><span data-stu-id="ef57a-172">After you create a self-signed certificate, you can sign scripts.</span></span> <span data-ttu-id="ef57a-173">Если вы используете политику выполнения **AllSigned** , подписывание сценария позволяет запустить сценарий на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ef57a-173">If you use the **AllSigned** execution policy, signing a script permits you to run the script on your computer.</span></span>

<span data-ttu-id="ef57a-174">Следующий пример скрипта `Add-Signature.ps1` подписывает скрипт.</span><span class="sxs-lookup"><span data-stu-id="ef57a-174">The following sample script, `Add-Signature.ps1`, signs a script.</span></span> <span data-ttu-id="ef57a-175">Однако при использовании политики выполнения **AllSigned** необходимо подписать `Add-Signature.ps1` сценарий перед запуском.</span><span class="sxs-lookup"><span data-stu-id="ef57a-175">However, if you are using the **AllSigned** execution policy, you must sign the `Add-Signature.ps1` script before you run it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef57a-176">Скрипт должен быть сохранен с использованием кодировки ASCII или UTF8NoBOM. Вы можете подписать файл сценария, который использует другую кодировку.</span><span class="sxs-lookup"><span data-stu-id="ef57a-176">The script must be saved using ASCII or UTF8NoBOM encoding.You can sign a script file that uses a different encoding.</span></span> <span data-ttu-id="ef57a-177">Но сценарий не запускается, или модуль, содержащий скрипт, не удается импортировать.</span><span class="sxs-lookup"><span data-stu-id="ef57a-177">But the script fails to run or the module containing the script fails to import.</span></span>

<span data-ttu-id="ef57a-178">Чтобы использовать этот сценарий, скопируйте следующий текст в текстовый файл и присвойте ему имя `Add-Signature.ps1` .</span><span class="sxs-lookup"><span data-stu-id="ef57a-178">To use this script, copy the following text into a text file, and name it `Add-Signature.ps1`.</span></span>

```powershell
## Signs a file
param([string] $file=$(throw "Please specify a filename."))
$cert = @(Get-ChildItem cert:\CurrentUser\My -codesigning)[0]
Set-AuthenticodeSignature $file $cert
```

<span data-ttu-id="ef57a-179">Чтобы подписать `Add-Signature.ps1` файл скрипта, введите в командной строке PowerShell следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ef57a-179">To sign the `Add-Signature.ps1` script file, type the following commands at the PowerShell command prompt:</span></span>

```powershell
$cert = @(Get-ChildItem cert:\CurrentUser\My -codesigning)[0]
Set-AuthenticodeSignature add-signature.ps1 $cert
```

<span data-ttu-id="ef57a-180">После подписания скрипта его можно запустить на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ef57a-180">After the script is signed, you can run it on the local computer.</span></span> <span data-ttu-id="ef57a-181">Однако сценарий не будет выполняться на компьютерах, на которых политика выполнения PowerShell требует наличия цифровой подписи от доверенного центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="ef57a-181">However, the script will not run on computers on which the PowerShell execution policy requires a digital signature from a trusted authority.</span></span> <span data-ttu-id="ef57a-182">При попытке PowerShell отобразится следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="ef57a-182">If you try, PowerShell displays the following error message:</span></span>

```Output
The file C:\remote_file.ps1 cannot be loaded. The signature of the
certificate cannot be verified.
At line:1 char:15
+ .\ remote_file.ps1 <<<<
```

<span data-ttu-id="ef57a-183">Если PowerShell отображает это сообщение при выполнении скрипта, который не был написан, обработайте файл так, как если бы вы ни использовали любой неподписанный сценарий.</span><span class="sxs-lookup"><span data-stu-id="ef57a-183">If PowerShell displays this message when you run a script that you did not write, treat the file as you would treat any unsigned script.</span></span> <span data-ttu-id="ef57a-184">Проверьте код, чтобы определить, можно ли доверять сценарию.</span><span class="sxs-lookup"><span data-stu-id="ef57a-184">Review the code to determine whether you can trust the script.</span></span>

## <a name="enable-strong-private-key-protection-for-your-certificate"></a><span data-ttu-id="ef57a-185">Включение усиленной защиты закрытого ключа для сертификата</span><span class="sxs-lookup"><span data-stu-id="ef57a-185">Enable strong private key protection for your certificate</span></span>

<span data-ttu-id="ef57a-186">При наличии частного сертификата на компьютере вредоносные программы могут подписывать сценарии от вашего имени, что позволяет PowerShell выполнять их.</span><span class="sxs-lookup"><span data-stu-id="ef57a-186">If you have a private certificate on your computer, malicious programs might be able to sign scripts on your behalf, which authorizes PowerShell to run them.</span></span>

<span data-ttu-id="ef57a-187">Чтобы предотвратить автоматический вход от вашего имени, используйте диспетчер сертификатов `Certmgr.exe` для экспорта сертификата подписи в `.pfx` файл.</span><span class="sxs-lookup"><span data-stu-id="ef57a-187">To prevent automated signing on your behalf, use Certificate Manager `Certmgr.exe` to export your signing certificate to a `.pfx` file.</span></span> <span data-ttu-id="ef57a-188">Диспетчер сертификатов входит в состав пакета SDK для Microsoft .NET, Microsoft Windows SDK и в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ef57a-188">Certificate Manager is included in the Microsoft .NET SDK, the Microsoft Windows SDK, and in internet Explorer.</span></span>

<span data-ttu-id="ef57a-189">Чтобы экспортировать сертификат, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef57a-189">To export the certificate:</span></span>

1. <span data-ttu-id="ef57a-190">Запустите диспетчер сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ef57a-190">Start Certificate Manager.</span></span>
2. <span data-ttu-id="ef57a-191">Выберите сертификат, выданный корневым каталогом локального сертификата PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef57a-191">Select the certificate issued by PowerShell Local Certificate Root.</span></span>
3. <span data-ttu-id="ef57a-192">Нажмите кнопку Экспорт, чтобы запустить мастер экспорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ef57a-192">Click Export to start the Certificate Export Wizard.</span></span>
4. <span data-ttu-id="ef57a-193">Выберите "Да, экспортировать закрытый ключ" и нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="ef57a-193">Select "Yes, export the private key", and then click Next.</span></span>
5. <span data-ttu-id="ef57a-194">Выберите "включить усиленную защиту".</span><span class="sxs-lookup"><span data-stu-id="ef57a-194">Select "Enable strong protection."</span></span>
6. <span data-ttu-id="ef57a-195">Введите пароль и введите его еще раз для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="ef57a-195">Type a password, and then type it again to confirm.</span></span>
7. <span data-ttu-id="ef57a-196">Введите имя файла с расширением имени PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="ef57a-196">Type a file name that has the .pfx file name extension.</span></span>
8. <span data-ttu-id="ef57a-197">Нажмите кнопку «Готово».</span><span class="sxs-lookup"><span data-stu-id="ef57a-197">Click Finish.</span></span>

<span data-ttu-id="ef57a-198">Чтобы повторно импортировать сертификат, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef57a-198">To re-import the certificate:</span></span>

1. <span data-ttu-id="ef57a-199">Запустите диспетчер сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ef57a-199">Start Certificate Manager.</span></span>
2. <span data-ttu-id="ef57a-200">Нажмите кнопку Импорт, чтобы запустить мастер импорта сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ef57a-200">Click Import to start the Certificate Import Wizard.</span></span>
3. <span data-ttu-id="ef57a-201">Откройте файл. pfx, созданный в процессе экспорта.</span><span class="sxs-lookup"><span data-stu-id="ef57a-201">Open to the location of the .pfx file that you created during the export process.</span></span>
4. <span data-ttu-id="ef57a-202">На странице Пароль выберите "включить усиленную защиту закрытого ключа", а затем введите пароль, назначенный в процессе экспорта.</span><span class="sxs-lookup"><span data-stu-id="ef57a-202">On the Password page, select "Enable strong private key protection", and then enter the password that you assigned during the export process.</span></span>
5. <span data-ttu-id="ef57a-203">Выберите хранилище личных сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ef57a-203">Select the Personal certificate store.</span></span>
6. <span data-ttu-id="ef57a-204">Нажмите кнопку «Готово».</span><span class="sxs-lookup"><span data-stu-id="ef57a-204">Click Finish.</span></span>

## <a name="prevent-the-signature-from-expiring"></a><span data-ttu-id="ef57a-205">Запрет истечения срока действия подписи</span><span class="sxs-lookup"><span data-stu-id="ef57a-205">Prevent the signature from expiring</span></span>

<span data-ttu-id="ef57a-206">Цифровая подпись в скрипте действительна до истечения срока действия сертификата подписи или до тех пор, пока сервер отметок времени не сможет проверить, подписан ли сценарий, пока сертификат для подписи был действителен.</span><span class="sxs-lookup"><span data-stu-id="ef57a-206">The digital signature in a script is valid until the signing certificate expires or as long as a timestamp server can verify that the script was signed while the signing certificate was valid.</span></span>

<span data-ttu-id="ef57a-207">Так как большинство сертификатов подписи действительны только в течение одного года, использование сервера отметок времени гарантирует, что пользователи смогут использовать ваш сценарий в течение многих лет.</span><span class="sxs-lookup"><span data-stu-id="ef57a-207">Because most signing certificates are valid for one year only, using a time stamp server ensures that users can use your script for many years to come.</span></span>

## <a name="see-also"></a><span data-ttu-id="ef57a-208">См. также</span><span class="sxs-lookup"><span data-stu-id="ef57a-208">See also</span></span>

[<span data-ttu-id="ef57a-209">about_Execution_Policies</span><span class="sxs-lookup"><span data-stu-id="ef57a-209">about_Execution_Policies</span></span>](about_Execution_Policies.md)

[<span data-ttu-id="ef57a-210">about_Profiles</span><span class="sxs-lookup"><span data-stu-id="ef57a-210">about_Profiles</span></span>](about_Profiles.md)

[<span data-ttu-id="ef57a-211">Get-ExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="ef57a-211">Get-ExecutionPolicy</span></span>](xref:Microsoft.PowerShell.Security.Get-ExecutionPolicy)

[<span data-ttu-id="ef57a-212">Set-ExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="ef57a-212">Set-ExecutionPolicy</span></span>](xref:Microsoft.PowerShell.Security.Set-ExecutionPolicy)

[<span data-ttu-id="ef57a-213">Set-AuthenticodeSignature</span><span class="sxs-lookup"><span data-stu-id="ef57a-213">Set-AuthenticodeSignature</span></span>](xref:Microsoft.PowerShell.Security.Set-AuthenticodeSignature)

<span data-ttu-id="ef57a-214">[Знакомство с подписыванием кода](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537361(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="ef57a-214">[Introduction to Code Signing](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537361(v=vs.85))</span></span>