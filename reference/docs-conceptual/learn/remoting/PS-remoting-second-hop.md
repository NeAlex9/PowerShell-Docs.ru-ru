---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Выполнение второго прыжка при удаленном взаимодействии PowerShell
ms.openlocfilehash: 06ca43e3e0524d89ec6f66f6553c4c75072beaf3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55680175"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a><span data-ttu-id="240de-103">Выполнение второго прыжка при удаленном взаимодействии PowerShell</span><span class="sxs-lookup"><span data-stu-id="240de-103">Making the second hop in PowerShell Remoting</span></span>

<span data-ttu-id="240de-104">"Проблема второго прыжка" относится к ситуации, аналогичной следующей:</span><span class="sxs-lookup"><span data-stu-id="240de-104">The "second hop problem" refers to a situation like the following:</span></span>

1. <span data-ttu-id="240de-105">Вы вошли на сервер _ServerA_.</span><span class="sxs-lookup"><span data-stu-id="240de-105">You are logged in to _ServerA_.</span></span>
2. <span data-ttu-id="240de-106">С сервера _ServerA_ вы запускаете удаленный сеанс PowerShell для подключения к серверу _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="240de-106">From _ServerA_, you start a remote PowerShell session to connect to _ServerB_.</span></span>
3. <span data-ttu-id="240de-107">Команда, запущенная вами на сервере _ServerB_ через сеанс удаленного взаимодействия PowerShell, пытается получить доступ к ресурсу на сервере _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="240de-107">A command you run on _ServerB_ via your PowerShell Remoting session attempts to access a resource on _ServerC_.</span></span>
4. <span data-ttu-id="240de-108">Доступ к ресурсу на _ServerC_ запрещен, так как учетные данные, используемые вами для создания сеанса удаленного взаимодействия PowerShell, не передаются с сервера _ServerB_ на сервер _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="240de-108">Access to the resource on _ServerC_ is denied, because the credentials you used to create the PowerShell Remoting session are not passed from _ServerB_ to _ServerC_.</span></span>

<span data-ttu-id="240de-109">Существует несколько способов для решения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="240de-109">There are several ways to address this problem.</span></span> <span data-ttu-id="240de-110">В этом разделе мы рассмотрим некоторые из наиболее популярных решений для проблемы второго прыжка.</span><span class="sxs-lookup"><span data-stu-id="240de-110">In this topic, we'll look at several of the most popular solutions to the second hop problem.</span></span>

## <a name="credssp"></a><span data-ttu-id="240de-111">CredSSP</span><span class="sxs-lookup"><span data-stu-id="240de-111">CredSSP</span></span>

<span data-ttu-id="240de-112">Для проверки подлинности можно использовать [протокол CredSSP](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx).</span><span class="sxs-lookup"><span data-stu-id="240de-112">You can use the [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) for authentication.</span></span> <span data-ttu-id="240de-113">Протокол CredSSP кэширует учетные данные на удаленном сервере (_ServerB_), что делает их уязвимыми для атак, направленных на кражу учетных данных.</span><span class="sxs-lookup"><span data-stu-id="240de-113">CredSSP caches credentials on the remote server (_ServerB_), so using it opens you up to credential theft attacks.</span></span> <span data-ttu-id="240de-114">Если безопасность удаленного компьютера нарушена, злоумышленник получает доступ к учетным данным пользователя.</span><span class="sxs-lookup"><span data-stu-id="240de-114">If the remote computer is compromised, the attacker has access to the user's credentials.</span></span> <span data-ttu-id="240de-115">Протокол CredSSP по умолчанию отключен на компьютерах клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="240de-115">CredSSP is disabled by default on both client and server computers.</span></span> <span data-ttu-id="240de-116">Включать протокол CredSSP следует только в самых надежных средах.</span><span class="sxs-lookup"><span data-stu-id="240de-116">You should enable CredSSP only in the most trusted environments.</span></span> <span data-ttu-id="240de-117">Например, при подключении администратора домена к контроллеру домена, так как контроллер домена является высоконадежным.</span><span class="sxs-lookup"><span data-stu-id="240de-117">For example, a domain administrator connecting to a domain controller because the domain controller is highly trusted.</span></span>

<span data-ttu-id="240de-118">Дополнительные сведения о вопросах безопасности при использовании протокола CredSSP для удаленного взаимодействия PowerShell см. в статье [Accidental Sabotage: Beware of CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp) (Непреднамеренный саботаж: берегитесь CredSSP).</span><span class="sxs-lookup"><span data-stu-id="240de-118">For more information about security concerns when using CredSSP for PowerShell Remoting, see [Accidental Sabotage: Beware of CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span></span>

<span data-ttu-id="240de-119">Дополнительные сведения об атаках, направленных на хищение учетных данных, см. в техническом документе [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span><span class="sxs-lookup"><span data-stu-id="240de-119">For more information about credential theft attacks, see [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span></span>

<span data-ttu-id="240de-120">Пример того, как включить и использовать CredSSP для удаленного взаимодействия PowerShell, см. в разделе [Использование CredSSP для решения проблемы второго прыжка](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span><span class="sxs-lookup"><span data-stu-id="240de-120">For an example of how to enable and use CredSSP for PowerShell remoting, see [Using CredSSP to solve the second-hop problem](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span></span>

### <a name="pros"></a><span data-ttu-id="240de-121">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-121">Pros</span></span>

- <span data-ttu-id="240de-122">Это работает для всех серверов с Windows Server 2008 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="240de-122">It works for all servers with Windows Server 2008 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="240de-123">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-123">Cons</span></span>

- <span data-ttu-id="240de-124">Имеет уязвимости.</span><span class="sxs-lookup"><span data-stu-id="240de-124">Has security vulnerabilities.</span></span>
- <span data-ttu-id="240de-125">Требует настройки как клиентских, так и серверных ролей.</span><span class="sxs-lookup"><span data-stu-id="240de-125">Requires configuration of both client and server roles.</span></span>

## <a name="kerberos-delegation-unconstrained"></a><span data-ttu-id="240de-126">Делегирование Kerberos (без ограничений)</span><span class="sxs-lookup"><span data-stu-id="240de-126">Kerberos delegation (unconstrained)</span></span>

<span data-ttu-id="240de-127">Для выполнения второго прыжка можно также использовать делегирование Kerberos без ограничений.</span><span class="sxs-lookup"><span data-stu-id="240de-127">You can also used Kerberos unconstrained delegation to make the second hop.</span></span> <span data-ttu-id="240de-128">Однако этот метод не позволяет управлять тем, где именно используются делегированные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="240de-128">However, this method provides no control of where delegated credentials are used.</span></span>

><span data-ttu-id="240de-129">**Примечание.** Учетные записи Active Directory, которые имеют набор свойств **Учетная запись важна и не может быть делегирована**, не могут быть делегированы.</span><span class="sxs-lookup"><span data-stu-id="240de-129">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="240de-130">Дополнительные сведения см. в разделе [Фокус безопасности: анализ свойств "Учетная запись важна и не может быть делегирована" для привилегированных учетных записей](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) и [Средства и параметры проверки подлинности Kerberos](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="240de-130">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="240de-131">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-131">Pros</span></span>

- <span data-ttu-id="240de-132">Не требует специального кода.</span><span class="sxs-lookup"><span data-stu-id="240de-132">Requires no special coding.</span></span>

### <a name="cons"></a><span data-ttu-id="240de-133">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-133">Cons</span></span>

- <span data-ttu-id="240de-134">Не поддерживает второй прыжок для WinRM.</span><span class="sxs-lookup"><span data-stu-id="240de-134">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="240de-135">Не позволяет управлять тем, где именно используются делегированные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="240de-135">Provides no control over where credentials are used, creating a security vulnerability.</span></span>

## <a name="kerberos-constrained-delegation"></a><span data-ttu-id="240de-136">Ограниченное делегирование Kerberos</span><span class="sxs-lookup"><span data-stu-id="240de-136">Kerberos constrained delegation</span></span>

<span data-ttu-id="240de-137">Для выполнения второго прыжка можно использовать устаревшее ограниченное делегирование (не на основе ресурсов).</span><span class="sxs-lookup"><span data-stu-id="240de-137">You can use legacy constrained delegation (not resource-based) to make the second hop.</span></span>

><span data-ttu-id="240de-138">**Примечание.** Учетные записи Active Directory, которые имеют набор свойств **Учетная запись важна и не может быть делегирована**, не могут быть делегированы.</span><span class="sxs-lookup"><span data-stu-id="240de-138">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="240de-139">Дополнительные сведения см. в разделе [Фокус безопасности: анализ свойств "Учетная запись важна и не может быть делегирована" для привилегированных учетных записей](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) и [Средства и параметры проверки подлинности Kerberos](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="240de-139">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="240de-140">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-140">Pros</span></span>

- <span data-ttu-id="240de-141">Не требует специального кода.</span><span class="sxs-lookup"><span data-stu-id="240de-141">Requires no special coding</span></span>

### <a name="cons"></a><span data-ttu-id="240de-142">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-142">Cons</span></span>

- <span data-ttu-id="240de-143">Не поддерживает второй прыжок для WinRM.</span><span class="sxs-lookup"><span data-stu-id="240de-143">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="240de-144">Требует настройки для объекта Active Directory удаленного сервера (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="240de-144">Must be configured on the Active Directory object of the remote server (_ServerB_).</span></span>
- <span data-ttu-id="240de-145">Ограничен одним доменом.</span><span class="sxs-lookup"><span data-stu-id="240de-145">Limited to one domain.</span></span> <span data-ttu-id="240de-146">Не может использоваться между доменами или лесами.</span><span class="sxs-lookup"><span data-stu-id="240de-146">Cannot cross domains or forests.</span></span>
- <span data-ttu-id="240de-147">Требует права на обновление объектов и имен субъектов-служб (SPN).</span><span class="sxs-lookup"><span data-stu-id="240de-147">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="240de-148">Ограниченное делегирование Kerberos на основе ресурсов</span><span class="sxs-lookup"><span data-stu-id="240de-148">Resource-based Kerberos constrained delegation</span></span>

<span data-ttu-id="240de-149">С помощью ограниченного делегирования Kerberos на основе ресурсов (которое впервые появилось в Windows Server 2012) можно настроить делегирование учетных данных на объект сервера, где находятся ресурсы.</span><span class="sxs-lookup"><span data-stu-id="240de-149">Using resource-based Kerberos constrained delegation (introduced in Windows Server 2012), you configure credential delegation on the server object where resources reside.</span></span>
<span data-ttu-id="240de-150">В описанном выше сценарии второго прыжка вы настраиваете сервер _ServerC_, чтобы указать, откуда он будет принимать делегированные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="240de-150">In the second hop scenario described above, you configure _ServerC_ to specify from where it will accept delegated credentials.</span></span>

><span data-ttu-id="240de-151">**Примечание.** Учетные записи Active Directory, которые имеют набор свойств **Учетная запись важна и не может быть делегирована**, не могут быть делегированы.</span><span class="sxs-lookup"><span data-stu-id="240de-151">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="240de-152">Дополнительные сведения см. в разделе [Фокус безопасности: анализ свойств "Учетная запись важна и не может быть делегирована" для привилегированных учетных записей](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) и [Средства и параметры проверки подлинности Kerberos](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="240de-152">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="240de-153">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-153">Pros</span></span>

- <span data-ttu-id="240de-154">Учетные данные не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="240de-154">Credentials are not stored.</span></span>
- <span data-ttu-id="240de-155">Относительно легок в настройке с помощью командлетов PowerShell — специальный код не требуется.</span><span class="sxs-lookup"><span data-stu-id="240de-155">Relatively easy to configure by using PowerShell cmdlets--no special coding required.</span></span>
- <span data-ttu-id="240de-156">Не требуется доступ к специальному домену.</span><span class="sxs-lookup"><span data-stu-id="240de-156">No special domain access is required.</span></span>
- <span data-ttu-id="240de-157">Работает между доменами и лесами.</span><span class="sxs-lookup"><span data-stu-id="240de-157">Works across domains and forests.</span></span>
- <span data-ttu-id="240de-158">Код PowerShell.</span><span class="sxs-lookup"><span data-stu-id="240de-158">PowerShell code.</span></span>

### <a name="cons"></a><span data-ttu-id="240de-159">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-159">Cons</span></span>

- <span data-ttu-id="240de-160">Требует Windows Server 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="240de-160">Requires Windows Server 2012 or later.</span></span>
- <span data-ttu-id="240de-161">Не поддерживает второй прыжок для WinRM.</span><span class="sxs-lookup"><span data-stu-id="240de-161">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="240de-162">Требует права на обновление объектов и имен субъектов-служб (SPN).</span><span class="sxs-lookup"><span data-stu-id="240de-162">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

### <a name="example"></a><span data-ttu-id="240de-163">Пример</span><span class="sxs-lookup"><span data-stu-id="240de-163">Example</span></span>

<span data-ttu-id="240de-164">Рассмотрим пример, в котором ограниченное делегирование на основе ресурсов PowerShell настраивается на сервере _ServerC_, чтобы разрешить использование делегированных учетных данных с сервера _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="240de-164">Let's look at a PowerShell example that configures resource based constrained delegation on _ServerC_ to allow delegated credentials from a _ServerB_.</span></span>
<span data-ttu-id="240de-165">В этом примере предполагается, что все серверы работают под управлением Windows Server 2012 или более поздней версии и существует по меньшей мере один контроллер домена Windows Server 2012 в каждом домене, к которому относятся какие-либо из серверов.</span><span class="sxs-lookup"><span data-stu-id="240de-165">This example assumes that all servers are running Windows Server 2012 or later, and that there is at least one Windows Server 2012 domain controller each domain to which any of the servers belong.</span></span>

<span data-ttu-id="240de-166">Перед настройкой ограниченного делегирования следует добавить компонент `RSAT-AD-PowerShell`, чтобы установить модуль Active Directory PowerShell, а затем импортировать этот модуль в сеанс:</span><span class="sxs-lookup"><span data-stu-id="240de-166">Before you can configure constrained delegation, you must add the `RSAT-AD-PowerShell` feature to install the Active Directory PowerShell module, and then import that module into your session:</span></span>

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirectory
```
<span data-ttu-id="240de-167">Сейчас параметр несколько доступных командлетов имеют параметр **PrincipalsAllowedToDelegateToAccount**:</span><span class="sxs-lookup"><span data-stu-id="240de-167">Several available cmdlets now have a **PrincipalsAllowedToDelegateToAccount** parameter:</span></span>

```powershell
PS C:\> Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount

CommandType Name                 ModuleName
----------- ----                 ----------
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

<span data-ttu-id="240de-168">Параметр **PrincipalsAllowedToDelegateToAccount** задает атрибут объекта Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity**, содержащий список управления доступом (ACL), который указывает, какие учетные записи имеют разрешение на делегирование учетных данных для связанной учетной записи (в нашем примере это будет учетная запись компьютера для _сервера_).</span><span class="sxs-lookup"><span data-stu-id="240de-168">The **PrincipalsAllowedToDelegateToAccount** parameter sets the Active Directory object attribute **msDS-AllowedToActOnBehalfOfOtherIdentity**, which contains an access control list (ACL) that specifies which accounts have permission to delegate credentials to the associated account (in our example, it will be the machine account for _Server_).</span></span>

<span data-ttu-id="240de-169">Теперь давайте настроим переменные, которые будем использовать для представления серверов:</span><span class="sxs-lookup"><span data-stu-id="240de-169">Now let's set up the variables we'll use to represent the servers:</span></span>

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

<span data-ttu-id="240de-170">WinRM (и поэтому удаленное взаимодействие PowerShell) по умолчанию выполняется как учетная запись компьютера.</span><span class="sxs-lookup"><span data-stu-id="240de-170">WinRM (and therefore PowerShell remoting) runs as the computer account by default.</span></span> <span data-ttu-id="240de-171">Это можно проверить, просмотрев свойство **StartName** службы `winrm`:</span><span class="sxs-lookup"><span data-stu-id="240de-171">You can see this by looking at the **StartName** property of the `winrm` service:</span></span>

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

<span data-ttu-id="240de-172">Чтобы сервер _ServerC_ разрешал делегирование из сеанса удаленного взаимодействия PowerShell на сервер _ServerB_, мы предоставим доступ, задав для параметра **PrincipalsAllowedToDelegateToAccount** на сервере _ServerC_ значение в виде объекта-компьютера сервера _ServerB_:</span><span class="sxs-lookup"><span data-stu-id="240de-172">For _ServerC_ to allow delegation from a PowerShell remoting session on _ServerB_, we will grant access by setting the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to the computer object of _ServerB_:</span></span>

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

<span data-ttu-id="240de-173">[Центр распространения ключей (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) Kerberos кэширует отклоненные попытки доступа (негативный кэш) в течение 15 минут.</span><span class="sxs-lookup"><span data-stu-id="240de-173">The Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) caches denied access attempts (negative cache) for 15 minutes.</span></span> <span data-ttu-id="240de-174">Если сервер _ServerB_ ранее пытался получить доступ к серверу _ServerC_, потребуется очистить кэш на сервере _ServerB_, вызвав следующую команду:</span><span class="sxs-lookup"><span data-stu-id="240de-174">If _ServerB_ has previously attempted to access _ServerC_, you will need to clear the cache on _ServerB_ by invoking the following command:</span></span>

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

<span data-ttu-id="240de-175">Можно также перезагрузить компьютер или подождать не менее 15 минут для очистки кэша.</span><span class="sxs-lookup"><span data-stu-id="240de-175">You could also restart the computer, or wait at least 15 minutes to clear the cache.</span></span>

<span data-ttu-id="240de-176">После очистки кэша можно запустить код с _ServerA_ через _ServerB_ и до _ServerC_:</span><span class="sxs-lookup"><span data-stu-id="240de-176">After clearing the cache, you can successfully run code from _ServerA_ through _ServerB_ to _ServerC_:</span></span>

```powershell
# Capture a credential
$cred = Get-Credential Contoso\Alice

# Test kerberos double hop
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    Test-Path \\$($using:ServerC.Name)\C$
    Get-Process lsass -ComputerName $($using:ServerC.Name)
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)
}
```

<span data-ttu-id="240de-177">В этом примере переменная `$using` используется, чтобы сделать переменную `$ServerC` видимой для сервера _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="240de-177">In this example, the `$using` variable is used to make the `$ServerC` variable visible to _ServerB_.</span></span> <span data-ttu-id="240de-178">Дополнительные сведения о переменной `$using` см. в разделе [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).</span><span class="sxs-lookup"><span data-stu-id="240de-178">For more information about the `$using` variable, see [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).</span></span>

<span data-ttu-id="240de-179">Чтобы разрешить нескольким серверам делегировать учетные данные серверу _ServerC_, задайте в качестве значения параметра **PrincipalsAllowedToDelegateToAccount** на сервере _ServerC_ в массив:</span><span class="sxs-lookup"><span data-stu-id="240de-179">To allow multiple servers to delegate credentials to _ServerC_, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to an array:</span></span>

```powershell
# Set up variables for each server
$ServerB1 = Get-ADComputer -Identity ServerB1
$ServerB2 = Get-ADComputer -Identity ServerB2
$ServerB3 = Get-ADComputer -Identity ServerB3
$ServerC  = Get-ADComputer -Identity ServerC

# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

<span data-ttu-id="240de-180">Если вы хотите сделать второй прыжок между доменами, добавьте полное доменное имя (FQDN) контроллера домена для того домена, к которому принадлежит _ServerB_:</span><span class="sxs-lookup"><span data-stu-id="240de-180">If you want to make the second hop across domains, add fully-qualified domain name (FQDN) of the domain controller of the domain to which _ServerB_ belongs:</span></span>

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

<span data-ttu-id="240de-181">Чтобы запретить нескольким серверам делегировать учетные данные серверу ServerC, задайте для параметра **PrincipalsAllowedToDelegateToAccount** на сервере _ServerC_ значение `$null`:</span><span class="sxs-lookup"><span data-stu-id="240de-181">To remove the ability to delegate credentials to ServerC, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to `$null`:</span></span>

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="240de-182">Информация об ограниченном делегировании Kerberos на основе ресурсов</span><span class="sxs-lookup"><span data-stu-id="240de-182">Information on resource-based Kerberos constrained delegation</span></span>

- [<span data-ttu-id="240de-183">Новые возможности проверки подлинности Kerberos</span><span class="sxs-lookup"><span data-stu-id="240de-183">What's New in Kerberos Authentication</span></span>](https://technet.microsoft.com/library/hh831747.aspx)
- [<span data-ttu-id="240de-184">Как Windows Server 2012 упрощает работу с ограниченным делегированием Kerberos, часть 1</span><span class="sxs-lookup"><span data-stu-id="240de-184">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 1</span></span>](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [<span data-ttu-id="240de-185">Как Windows Server 2012 упрощает работу с ограниченным делегированием Kerberos, часть 2</span><span class="sxs-lookup"><span data-stu-id="240de-185">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 2</span></span>](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [<span data-ttu-id="240de-186">Основные сведения об ограниченном делегировании Kerberos для развертывания прокси приложения Azure Active Directory со встроенной проверкой подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="240de-186">Understanding Kerberos Constrained Delegation for Azure Active Directory Application Proxy Deployments with Integrated Windows Authentication</span></span>](https://aka.ms/kcdpaper)
- <span data-ttu-id="240de-187">[[MS-ADA2]. Атрибуты M2.210 схемы Active Directory msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)</span><span class="sxs-lookup"><span data-stu-id="240de-187">[[MS-ADA2]: Active Directory Schema Attributes M2.210 Attribute msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)</span></span>
- <span data-ttu-id="240de-188">[[MS-SFU]. Расширения протокола Kerberos: S4U и протокола ограниченного делегирования 1.3.2 S4U2proxy](https://msdn.microsoft.com/library/cc246079.aspx)</span><span class="sxs-lookup"><span data-stu-id="240de-188">[[MS-SFU]: Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol 1.3.2 S4U2proxy](https://msdn.microsoft.com/library/cc246079.aspx)</span></span>
- [<span data-ttu-id="240de-189">Ограниченное делегирование Kerberos на основе ресурсов</span><span class="sxs-lookup"><span data-stu-id="240de-189">Resource Based Kerberos Constrained Delegation</span></span>](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [<span data-ttu-id="240de-190">Удаленное администрирование без ограниченного делегирования с помощью PrincipalsAllowedToDelegateToAccount</span><span class="sxs-lookup"><span data-stu-id="240de-190">Remote Administration Without Constrained Delegation Using PrincipalsAllowedToDelegateToAccount</span></span>](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a><span data-ttu-id="240de-191">PSSessionConfiguration с использованием RunAs</span><span class="sxs-lookup"><span data-stu-id="240de-191">PSSessionConfiguration using RunAs</span></span>

<span data-ttu-id="240de-192">Можно создать конфигурацию сеанса на сервере _ServerB_ и задать ее параметр **RunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="240de-192">You can create a session configuration on _ServerB_ and set its **RunAsCredential** parameter.</span></span>

<span data-ttu-id="240de-193">Сведения об использовании PSSessionConfiguration и RunAs для решения проблемы второго прыжка см. в разделе [Другое решение для удаленного взаимодействия PowerShell с несколькими прыжками](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span><span class="sxs-lookup"><span data-stu-id="240de-193">For information about using PSSessionConfiguration and RunAs to solve the second hop problem, see [Another solution to multi-hop PowerShell remoting](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span></span>

### <a name="pros"></a><span data-ttu-id="240de-194">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-194">Pros</span></span>

- <span data-ttu-id="240de-195">Работает для любого сервера с WMF 3.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="240de-195">Works with any server with WMF 3.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="240de-196">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-196">Cons</span></span>

- <span data-ttu-id="240de-197">Требует настройки **PSSessionConfiguration** и **RunAs** на каждом промежуточном сервере (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="240de-197">Requires configuration of **PSSessionConfiguration** and **RunAs** on every intermediate server (_ServerB_).</span></span>
- <span data-ttu-id="240de-198">Требуется обслуживание паролей при использовании учетной записи **запуска от имени** домена.</span><span class="sxs-lookup"><span data-stu-id="240de-198">Requires password maintenance when using a domain **RunAs** account</span></span>

## <a name="just-enough-administration-jea"></a><span data-ttu-id="240de-199">Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="240de-199">Just Enough Administration (JEA)</span></span>

<span data-ttu-id="240de-200">JEA позволяет ограничить команды, доступные администратору во время сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="240de-200">JEA allows you to restrict what commands an administrator can run during a PowerShell session.</span></span> <span data-ttu-id="240de-201">Это позволяет решить проблему второго прыжка.</span><span class="sxs-lookup"><span data-stu-id="240de-201">It can be used to solve the second hop problem.</span></span>

<span data-ttu-id="240de-202">Сведения о JEA см. в разделе [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).</span><span class="sxs-lookup"><span data-stu-id="240de-202">For information about JEA, see [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).</span></span>

### <a name="pros"></a><span data-ttu-id="240de-203">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-203">Pros</span></span>

- <span data-ttu-id="240de-204">При использовании виртуальной учетной записи обслуживание паролей не требуется.</span><span class="sxs-lookup"><span data-stu-id="240de-204">No password maintenance when using a virtual account.</span></span>

### <a name="cons"></a><span data-ttu-id="240de-205">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-205">Cons</span></span>

- <span data-ttu-id="240de-206">Требуется WMF 5.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="240de-206">Requires WMF 5.0 or later.</span></span>
- <span data-ttu-id="240de-207">Требует настройки на каждом промежуточном сервере (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="240de-207">Requires configuration on every intermediate server (_ServerB_).</span></span>

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a><span data-ttu-id="240de-208">Передача учетных данных внутри блока сценария Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="240de-208">Pass credentials inside an Invoke-Command script block</span></span>

<span data-ttu-id="240de-209">Можно передать учетные данные внутри параметра **ScriptBlock** вызова командлета [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command).</span><span class="sxs-lookup"><span data-stu-id="240de-209">You can pass credentials inside the **ScriptBlock** parameter of a call to the [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) cmdlet.</span></span>

### <a name="pros"></a><span data-ttu-id="240de-210">Плюсы</span><span class="sxs-lookup"><span data-stu-id="240de-210">Pros</span></span>

- <span data-ttu-id="240de-211">Не требуется специальной настройки серверов.</span><span class="sxs-lookup"><span data-stu-id="240de-211">Does not require special server configuration.</span></span>
- <span data-ttu-id="240de-212">Работает на любом сервере с WMF 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="240de-212">Works on any server running WMF 2.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="240de-213">Минусы</span><span class="sxs-lookup"><span data-stu-id="240de-213">Cons</span></span>

- <span data-ttu-id="240de-214">Требует внимательного составления кода.</span><span class="sxs-lookup"><span data-stu-id="240de-214">Requires an awkward code technique.</span></span>
- <span data-ttu-id="240de-215">При использовании WMF 2.0 требуется использовать иной синтаксис для передачи аргументов в удаленный сеанс.</span><span class="sxs-lookup"><span data-stu-id="240de-215">If running WMF 2.0, requires different syntax for passing arguments to a remote session.</span></span>

### <a name="example"></a><span data-ttu-id="240de-216">Пример</span><span class="sxs-lookup"><span data-stu-id="240de-216">Example</span></span>

<span data-ttu-id="240de-217">Следующий пример показывает, как передать учетные данные внутри блока сценария **Invoke-Command**:</span><span class="sxs-lookup"><span data-stu-id="240de-217">The following example shows how to pass credentials in an **Invoke-Command** script block:</span></span>

```powershell
# This works without delegation, passing fresh creds
# Note $Using:Cred in nested request
$cred = Get-Credential Contoso\Administrator
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {
    hostname
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}
}
```

## <a name="see-also"></a><span data-ttu-id="240de-218">См. также:</span><span class="sxs-lookup"><span data-stu-id="240de-218">See also</span></span>

[<span data-ttu-id="240de-219">Вопросы обеспечения безопасности для удаленного взаимодействия PowerShell</span><span class="sxs-lookup"><span data-stu-id="240de-219">PowerShell Remoting Security Considerations</span></span>](WinRMSecurity.md)