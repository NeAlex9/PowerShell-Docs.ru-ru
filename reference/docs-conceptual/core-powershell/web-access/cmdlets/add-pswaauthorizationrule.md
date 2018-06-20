---
ms.topic: reference
keywords: powershell,командлет
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: b8020f8b034ab24d79a96da3908e9b63bf017cd9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190389"
---
# <a name="add-pswaauthorizationrule"></a><span data-ttu-id="81c65-103">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="81c65-103">Add-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="81c65-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="81c65-104">SYNOPSIS</span></span>

<span data-ttu-id="81c65-105">Добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="81c65-105">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="syntax"></a><span data-ttu-id="81c65-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="81c65-106">Syntax</span></span>

### <a name="usergroupnamecomputergroupname"></a><span data-ttu-id="81c65-107">UserGroupNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="81c65-107">UserGroupNameComputerGroupName</span></span>
```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a><span data-ttu-id="81c65-108">UserGroupNameComputerName</span><span class="sxs-lookup"><span data-stu-id="81c65-108">UserGroupNameComputerName</span></span>
```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a><span data-ttu-id="81c65-109">UserNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="81c65-109">UserNameComputerGroupName</span></span>
```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a><span data-ttu-id="81c65-110">UserNameComputerName</span><span class="sxs-lookup"><span data-stu-id="81c65-110">UserNameComputerName</span></span>
```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="81c65-111">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="81c65-111">DESCRIPTION</span></span>

<span data-ttu-id="81c65-112">Командлет **Add-PswaAuthorizationRule** добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="81c65-112">The **Add-PswaAuthorizationRule** cmdlet adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

<span data-ttu-id="81c65-113">Для этого правила необходимо указать пользователей, компьютеры и конечные точки Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81c65-113">You must specify the users, computers, and Windows PowerShell endpoints for this rule.</span></span> <span data-ttu-id="81c65-114">Можно указать пользователей и компьютеры по отдельности (имена учетных записей и имена компьютеров) или задать группу.</span><span class="sxs-lookup"><span data-stu-id="81c65-114">You can specify both users and computers either by individual user accounts and computer names, or by specifying groups.</span></span>

<span data-ttu-id="81c65-115">Чтобы создать правило для компьютера, который присоединен к домену Active Directory, командлет использует идентификатор безопасности (SID) этого компьютера.</span><span class="sxs-lookup"><span data-stu-id="81c65-115">For a computer that is joined to an Active Directory domain, the cmdlet uses the security identifier (SID) of the computer to create the rule.</span></span>
<span data-ttu-id="81c65-116">Это позволяет указать в поле **Имя компьютера** на странице входа короткое имя, полное доменное имя или IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="81c65-116">This allows you to use a short name, a fully qualified domain name (FQDN), or an IP address for the **Computer Name** field on the sign-in page.</span></span>

<span data-ttu-id="81c65-117">Для компьютера, который не присоединен к домену Active Directory, командлет создает правило, используя имя компьютера, предоставленное администратором.</span><span class="sxs-lookup"><span data-stu-id="81c65-117">For a computer that is not joined to an Active Directory domain, the cmdlet creates the rule using the computer name provided by the administrator.</span></span> <span data-ttu-id="81c65-118">Для успешного подключения к этому компьютеру конечному пользователю необходимо указать имя компьютера точно так, как оно отображается в правиле.</span><span class="sxs-lookup"><span data-stu-id="81c65-118">To successfully connect to this machine, the end user must provide the computer name exactly as it appears in the rule.</span></span>

<span data-ttu-id="81c65-119">При наличии в сети нескольких компьютеров с одним именем короткое имя можно разрешить в несколько компьютеров.</span><span class="sxs-lookup"><span data-stu-id="81c65-119">If there are multiple computers with the same name on the network, then short name can resolve to more than one computer.</span></span> <span data-ttu-id="81c65-120">Это может привести к неоднозначности при установке подключения.</span><span class="sxs-lookup"><span data-stu-id="81c65-120">This can lead to ambiguity when establishing a connection.</span></span> <span data-ttu-id="81c65-121">Например, если правило существует для компьютера рабочей группы с именем *Server1* и к сети подключается новый компьютер с именем *server1.contoso.com*, проверка с помощью правил авторизации выполняется успешно и Windows PowerShell Web Access пытается установить подключение к компьютеру с именем *Server1*.</span><span class="sxs-lookup"><span data-stu-id="81c65-121">For example, if a rule exists for the workgroup computer named "*Server1*” and a new computer named *server1.contoso.com* is joined to the network, validation using the authorization rules succeeds and Windows PowerShell Web Access attempts to establish a connection to the computer named “*Server1*”.</span></span> <span data-ttu-id="81c65-122">Но нет никакой гарантии, что подключение будет установлено с указанным компьютером рабочей группы: попытка будет выполняться как для компьютера в рабочей группе, так и для компьютера домена с именем *Server1*.</span><span class="sxs-lookup"><span data-stu-id="81c65-122">It is not guaranteed that the connection is established with the specified workgroup computer; the attempt could be made on either the workgroup or the domain computer named "*Server1*".</span></span> <span data-ttu-id="81c65-123">Чтобы избежать неоднозначности, для создания правил авторизации рекомендуется по возможности использовать полное доменное имя целевого компьютера.</span><span class="sxs-lookup"><span data-stu-id="81c65-123">To reduce ambiguity, it is recommended that you use the FQDN for the destination computer whenever possible to create an authorization rule.</span></span>

<span data-ttu-id="81c65-124">Правила авторизации проверяют основные учетные данные пользователей Windows PowerShell Web Access, а не альтернативные учетные данные (второй набор учетных данных содержится в разделе **Дополнительные параметры подключения** на странице входа).</span><span class="sxs-lookup"><span data-stu-id="81c65-124">The authorization rules evaluate the primary sign-in credential of the Windows PowerShell Web Access users, not the alternate credentials (the second set of credentials found in the **Optional connection settings** section of the sign-in page).</span></span> <span data-ttu-id="81c65-125">Дополнительные сведения см. в примере 6.</span><span class="sxs-lookup"><span data-stu-id="81c65-125">For an example of this, see Example 6.</span></span>

## <a name="parameters"></a><span data-ttu-id="81c65-126">Параметры</span><span class="sxs-lookup"><span data-stu-id="81c65-126">Parameters</span></span>

### <a name="-computergroupnameltstringgt"></a><span data-ttu-id="81c65-127">-ComputerGroupName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-127">-ComputerGroupName&lt;String&gt;</span></span>

<span data-ttu-id="81c65-128">Указывает имя группы компьютеров в доменных службах Active Directory (AD DS) или локальных группах, к которым это правило предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="81c65-128">Specifies the name of a computer group in Active Directory Domain Services (AD DS) or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-129">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-129">Aliases</span></span>                              | <span data-ttu-id="81c65-130">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-130">none</span></span>                                 |
| <span data-ttu-id="81c65-131">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-131">Required?</span></span>                            | <span data-ttu-id="81c65-132">верно</span><span class="sxs-lookup"><span data-stu-id="81c65-132">true</span></span>                                 |
| <span data-ttu-id="81c65-133">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-133">Position?</span></span>                            | <span data-ttu-id="81c65-134">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-134">named</span></span>                                |
| <span data-ttu-id="81c65-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-135">Default Value</span></span>                        | <span data-ttu-id="81c65-136">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-136">none</span></span>                                 |
| <span data-ttu-id="81c65-137">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-138">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="81c65-138">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="81c65-139">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-140">false</span><span class="sxs-lookup"><span data-stu-id="81c65-140">false</span></span>                                |

### <a name="-computernameltstringgt"></a><span data-ttu-id="81c65-141">-ComputerName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-141">-ComputerName&lt;String&gt;</span></span>

<span data-ttu-id="81c65-142">Указывает имя компьютера, к которому это правило предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="81c65-142">Specifies the computer name to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-143">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-143">Aliases</span></span>                              | <span data-ttu-id="81c65-144">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-144">none</span></span>                                 |
| <span data-ttu-id="81c65-145">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-145">Required?</span></span>                            | <span data-ttu-id="81c65-146">верно</span><span class="sxs-lookup"><span data-stu-id="81c65-146">true</span></span>                                 |
| <span data-ttu-id="81c65-147">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-147">Position?</span></span>                            | <span data-ttu-id="81c65-148">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-148">named</span></span>                                |
| <span data-ttu-id="81c65-149">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-149">Default Value</span></span>                        | <span data-ttu-id="81c65-150">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-150">none</span></span>                                 |
| <span data-ttu-id="81c65-151">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-152">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="81c65-152">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="81c65-153">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-154">false</span><span class="sxs-lookup"><span data-stu-id="81c65-154">false</span></span>                                |

### <a name="-configurationnameltstringgt"></a><span data-ttu-id="81c65-155">-ConfigurationName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-155">-ConfigurationName&lt;String&gt;</span></span>

<span data-ttu-id="81c65-156">Указывает имя конфигурации сеанса Windows PowerShell (также известной как пространство выполнения), к которой это правило предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="81c65-156">Specifies the name of the Windows PowerShell session configuration, also known as runspace, to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-157">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-157">Aliases</span></span>                              | <span data-ttu-id="81c65-158">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-158">none</span></span>                                 |
| <span data-ttu-id="81c65-159">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-159">Required?</span></span>                            | <span data-ttu-id="81c65-160">верно</span><span class="sxs-lookup"><span data-stu-id="81c65-160">true</span></span>                                 |
| <span data-ttu-id="81c65-161">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-161">Position?</span></span>                            | <span data-ttu-id="81c65-162">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-162">named</span></span>                                |
| <span data-ttu-id="81c65-163">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-163">Default Value</span></span>                        | <span data-ttu-id="81c65-164">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-164">none</span></span>                                 |
| <span data-ttu-id="81c65-165">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-165">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-166">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="81c65-166">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="81c65-167">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-167">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-168">false</span><span class="sxs-lookup"><span data-stu-id="81c65-168">false</span></span>                                |

### <a name="-credentialltpscredentialgt"></a><span data-ttu-id="81c65-169">-Credential&lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-169">-Credential&lt;PSCredential&gt;</span></span>

<span data-ttu-id="81c65-170">Указывает объект **PSCredential** для учетной записи пользователя, который предполагается использовать для изменения правил авторизации Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="81c65-170">Specifies a **PSCredential** object for a user account that you want to use to change Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="81c65-171">Если этот параметр не добавлен, командлет будет использовать учетную запись текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="81c65-171">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="81c65-172">Чтобы получить объект **PSCredential**, который требуется для удаленного добавления правил авторизации, запустите командлет [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="81c65-172">To get a **PSCredential** object, which is required to add authorization rules remotely, run the [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-173">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-173">Aliases</span></span>                              | <span data-ttu-id="81c65-174">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-174">none</span></span>                                 |
| <span data-ttu-id="81c65-175">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-175">Required?</span></span>                            | <span data-ttu-id="81c65-176">false</span><span class="sxs-lookup"><span data-stu-id="81c65-176">false</span></span>                                |
| <span data-ttu-id="81c65-177">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-177">Position?</span></span>                            | <span data-ttu-id="81c65-178">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-178">named</span></span>                                |
| <span data-ttu-id="81c65-179">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-179">Default Value</span></span>                        | <span data-ttu-id="81c65-180">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-180">none</span></span>                                 |
| <span data-ttu-id="81c65-181">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-181">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-182">false</span><span class="sxs-lookup"><span data-stu-id="81c65-182">false</span></span>                                |
| <span data-ttu-id="81c65-183">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-183">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-184">false</span><span class="sxs-lookup"><span data-stu-id="81c65-184">false</span></span>                                |

### <a name="-force"></a><span data-ttu-id="81c65-185">-Force</span><span class="sxs-lookup"><span data-stu-id="81c65-185">-Force</span></span>

<span data-ttu-id="81c65-186">Принудительное выполнение команды без запроса на подтверждение пользователем.</span><span class="sxs-lookup"><span data-stu-id="81c65-186">Forces the command to run without asking for user confirmation.\\</span></span>
<span data-ttu-id="81c65-187">Кроме того, выводится запрос на подтверждение при вводе простого или короткого имени компьютера (например, имени, которое не является именем домена или указано не полностью).</span><span class="sxs-lookup"><span data-stu-id="81c65-187">In addition, it also prompts for confirmation when you enter a simple or short computer name (such as a name that is not a domain name or is not fully qualified).</span></span> <span data-ttu-id="81c65-188">Подтверждение запрашивается из соображений безопасности, чтобы простое имя можно было использовать для добавления компьютера только в том случае, если компьютер входит в рабочую группу.</span><span class="sxs-lookup"><span data-stu-id="81c65-188">Confirmation is requested for security reasons, so that you can use the simple name to add a computer only if the computer is in a workgroup.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-189">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-189">Aliases</span></span>                              | <span data-ttu-id="81c65-190">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-190">none</span></span>                                 |
| <span data-ttu-id="81c65-191">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-191">Required?</span></span>                            | <span data-ttu-id="81c65-192">false</span><span class="sxs-lookup"><span data-stu-id="81c65-192">false</span></span>                                |
| <span data-ttu-id="81c65-193">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-193">Position?</span></span>                            | <span data-ttu-id="81c65-194">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-194">named</span></span>                                |
| <span data-ttu-id="81c65-195">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-195">Default Value</span></span>                        | <span data-ttu-id="81c65-196">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-196">none</span></span>                                 |
| <span data-ttu-id="81c65-197">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-197">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-198">false</span><span class="sxs-lookup"><span data-stu-id="81c65-198">false</span></span>                                |
| <span data-ttu-id="81c65-199">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-199">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-200">false</span><span class="sxs-lookup"><span data-stu-id="81c65-200">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="81c65-201">-RuleName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-201">-RuleName&lt;String&gt;</span></span>

<span data-ttu-id="81c65-202">Задает понятное имя для этого правила.</span><span class="sxs-lookup"><span data-stu-id="81c65-202">Specifies the friendly name for this rule.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-203">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-203">Aliases</span></span>                              | <span data-ttu-id="81c65-204">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-204">none</span></span>                                 |
| <span data-ttu-id="81c65-205">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-205">Required?</span></span>                            | <span data-ttu-id="81c65-206">false</span><span class="sxs-lookup"><span data-stu-id="81c65-206">false</span></span>                                |
| <span data-ttu-id="81c65-207">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-207">Position?</span></span>                            | <span data-ttu-id="81c65-208">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-208">named</span></span>                                |
| <span data-ttu-id="81c65-209">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-209">Default Value</span></span>                        | <span data-ttu-id="81c65-210">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-210">none</span></span>                                 |
| <span data-ttu-id="81c65-211">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-211">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-212">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="81c65-212">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="81c65-213">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-213">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-214">false</span><span class="sxs-lookup"><span data-stu-id="81c65-214">false</span></span>                                |

### <a name="-usergroupnameltstringgt"></a><span data-ttu-id="81c65-215">-UserGroupName&lt;строка\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-215">-UserGroupName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="81c65-216">Указывает имя одной или нескольких групп пользователей в AD DS или локальных группах, к которым это правило предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="81c65-216">Specifies the name of one or more user groups in AD DS or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-217">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-217">Aliases</span></span>                              | <span data-ttu-id="81c65-218">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-218">none</span></span>                                 |
| <span data-ttu-id="81c65-219">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-219">Required?</span></span>                            | <span data-ttu-id="81c65-220">верно</span><span class="sxs-lookup"><span data-stu-id="81c65-220">true</span></span>                                 |
| <span data-ttu-id="81c65-221">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-221">Position?</span></span>                            | <span data-ttu-id="81c65-222">с именем</span><span class="sxs-lookup"><span data-stu-id="81c65-222">named</span></span>                                |
| <span data-ttu-id="81c65-223">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-223">Default Value</span></span>                        | <span data-ttu-id="81c65-224">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-224">none</span></span>                                 |
| <span data-ttu-id="81c65-225">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-225">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-226">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="81c65-226">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="81c65-227">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-227">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-228">false</span><span class="sxs-lookup"><span data-stu-id="81c65-228">false</span></span>                                |

### <a name="-usernameltstringgt"></a><span data-ttu-id="81c65-229">-UserName&lt;строка\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-229">-UserName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="81c65-230">Указывает одного или нескольких пользователей, к которым это правило предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="81c65-230">Specifies one or more users to which this rule grants access.</span></span> <span data-ttu-id="81c65-231">Имя пользователя может быть локальной учетной записью пользователя на компьютере шлюза или пользователем в доменных службах Active Directory.</span><span class="sxs-lookup"><span data-stu-id="81c65-231">The user name can be a local user account on the gateway computer or a user in AD DS.</span></span>
<span data-ttu-id="81c65-232">Формат: `domain\user` или `computer\user`.</span><span class="sxs-lookup"><span data-stu-id="81c65-232">The format is `domain\user` or `computer\user`.</span></span>

|||
|-|-|
| <span data-ttu-id="81c65-233">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="81c65-233">Aliases</span></span>                              | <span data-ttu-id="81c65-234">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-234">none</span></span>                                 |
| <span data-ttu-id="81c65-235">Требуется?</span><span class="sxs-lookup"><span data-stu-id="81c65-235">Required?</span></span>                            | <span data-ttu-id="81c65-236">верно</span><span class="sxs-lookup"><span data-stu-id="81c65-236">true</span></span>                                 |
| <span data-ttu-id="81c65-237">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="81c65-237">Position?</span></span>                            | <span data-ttu-id="81c65-238">1</span><span class="sxs-lookup"><span data-stu-id="81c65-238">1</span></span>                                    |
| <span data-ttu-id="81c65-239">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="81c65-239">Default Value</span></span>                        | <span data-ttu-id="81c65-240">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="81c65-240">none</span></span>                                 |
| <span data-ttu-id="81c65-241">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="81c65-241">Accept Pipeline Input?</span></span>               | <span data-ttu-id="81c65-242">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="81c65-242">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="81c65-243">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="81c65-243">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="81c65-244">false</span><span class="sxs-lookup"><span data-stu-id="81c65-244">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="81c65-245">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="81c65-245">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="81c65-246">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="81c65-246">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="81c65-247">Дополнительные сведения см. в разделе [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span><span class="sxs-lookup"><span data-stu-id="81c65-247">For more information, see [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span></span>

## <a name="inputs"></a><span data-ttu-id="81c65-248">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="81c65-248">INPUTS</span></span>

### <a name="string"></a><span data-ttu-id="81c65-249">Строка</span><span class="sxs-lookup"><span data-stu-id="81c65-249">String</span></span>

<span data-ttu-id="81c65-250">Этот командлет принимает в качестве входных данных строку или массив строк.</span><span class="sxs-lookup"><span data-stu-id="81c65-250">This cmdlet accepts a string or an array of strings as input.</span></span>

### <a name="string"></a><span data-ttu-id="81c65-251">String\[\]</span><span class="sxs-lookup"><span data-stu-id="81c65-251">String\[\]</span></span>

<span data-ttu-id="81c65-252">Этот командлет принимает в качестве входных данных строку или массив строк.</span><span class="sxs-lookup"><span data-stu-id="81c65-252">This cmdlet accepts a string or an array of strings as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="81c65-253">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="81c65-253">Outputs</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="81c65-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="81c65-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span></span>

<span data-ttu-id="81c65-255">Этот командлет возвращает объект правила авторизации.</span><span class="sxs-lookup"><span data-stu-id="81c65-255">This cmdlet returns the an authorization rule object.</span></span>

## <a name="examples"></a><span data-ttu-id="81c65-256">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="81c65-256">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="81c65-257">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="81c65-257">EXAMPLE 1</span></span>

<span data-ttu-id="81c65-258">В этом примере предоставляется доступ к конфигурации сеанса *PSWAEndpoint*, ограниченному пространству выполнения, на сервере *srv2* для пользователей в группе *SMAdmins*.</span><span class="sxs-lookup"><span data-stu-id="81c65-258">This example grants access to the session configuration *PSWAEndpoint*, a restricted runspace, on *srv2* for users in the *SMAdmins* group.\\</span></span>
<span data-ttu-id="81c65-259">**Примечание**. Имя компьютера должно указываться в виде полного доменного имени.</span><span class="sxs-lookup"><span data-stu-id="81c65-259">**Note**: The computer name must be a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="81c65-260">Администраторы определяют ограниченную конфигурацию сеанса или пространства выполнения, то есть ограниченный набор командлетов и задач, которые могут выполнять конечные пользователи.</span><span class="sxs-lookup"><span data-stu-id="81c65-260">Administrators define a restricted session configuration or runspace, which is a limited range of cmdlets and tasks that end users can run.</span></span> <span data-ttu-id="81c65-261">Определение ограниченного пространства выполнения блокирует доступ пользователей к другим компьютерам, которые находятся за пределами разрешенного пространства выполнения Windows PowerShell®, тем самым обеспечивая более безопасное подключение.</span><span class="sxs-lookup"><span data-stu-id="81c65-261">Defining a restricted runspace can prevent users from accessing other computers that are not in the allowed Windows PowerShell® runspace, thus offering a more secure connection.</span></span> <span data-ttu-id="81c65-262">Дополнительные сведения о конфигурациях сеансов см. в разделе [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) или [Установка и использование Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="81c65-262">For more information on session configurations, see [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) or the [Install and Use Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span></span>

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a><span data-ttu-id="81c65-263">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="81c65-263">EXAMPLE 2</span></span>

<span data-ttu-id="81c65-264">В этом примере предоставляется доступ к конфигурации сеанса Windows PowerShell по умолчанию, `Microsoft.PowerShell` на сервере *srv2* для пользователей с именем contoso\\user1, contoso\\user2 и contoso\\user3.</span><span class="sxs-lookup"><span data-stu-id="81c65-264">This example grants access to the default Windows PowerShell session configuration, `Microsoft.PowerShell`, on *srv2* for users in the users named contoso\\user1, contoso\\user2, and contoso\\user3.</span></span> <span data-ttu-id="81c65-265">Этот командлет создает три правила (по одному на каждого человека).</span><span class="sxs-lookup"><span data-stu-id="81c65-265">This cmdlet creates three rules (1 per person).</span></span>

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a><span data-ttu-id="81c65-266">ПРИМЕР 3</span><span class="sxs-lookup"><span data-stu-id="81c65-266">EXAMPLE 3</span></span>

<span data-ttu-id="81c65-267">В этом примере показано, как вводить значения имен пользователей через конвейер.</span><span class="sxs-lookup"><span data-stu-id="81c65-267">This example illustrates how to input user name values via the pipeline.</span></span>

```
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a><span data-ttu-id="81c65-268">ПРИМЕР 4</span><span class="sxs-lookup"><span data-stu-id="81c65-268">EXAMPLE 4</span></span>

<span data-ttu-id="81c65-269">В этом примере показано, как все параметры принимают значения из конвейера по имени свойства.</span><span class="sxs-lookup"><span data-stu-id="81c65-269">This example illustrates how all parameters take values from pipeline by property name.</span></span>

````PowerShell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a><span data-ttu-id="81c65-270">ПРИМЕР 5</span><span class="sxs-lookup"><span data-stu-id="81c65-270">EXAMPLE 5</span></span>

<span data-ttu-id="81c65-271">В этом примере добавляется правило, которое предоставляет локальному пользователю с именем *PswaServer\\ChrisLocal* доступ к серверу с именем *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="81c65-271">This example adds a rule to allow the local user named *PswaServer\\ChrisLocal* access to the server named *srv1.contoso.com*.</span></span>

<span data-ttu-id="81c65-272">В этом примере показана ситуация, в которой шлюз находится в рабочей группе, а целевой компьютер входит в домен.</span><span class="sxs-lookup"><span data-stu-id="81c65-272">This example illustrates a scenario where the gateway is in a workgroup and the destination computer is in a domain.</span></span> <span data-ttu-id="81c65-273">Правило авторизации применяется к локальным пользователям на сервере шлюза.</span><span class="sxs-lookup"><span data-stu-id="81c65-273">The authorization rule applies to the local users on the gateway.</span></span> <span data-ttu-id="81c65-274">На странице входа Windows PowerShell Web Access для успешного прохождения проверки подлинности пользователь должен предоставить второй набор учетных данных в области **Дополнительные параметры подключения**.</span><span class="sxs-lookup"><span data-stu-id="81c65-274">On the Windows PowerShell Web Access sign-in page, to successfully authenticate, the user must provide a second set of credentials in the **Optional connection settings** area.</span></span> <span data-ttu-id="81c65-275">Сервер шлюза использует этот дополнительный набор учетных данных для проверки подлинности пользователя на конечном компьютере (сервере *srv1.contoso.com*).</span><span class="sxs-lookup"><span data-stu-id="81c65-275">The gateway server uses the additional set of credentials to authenticate the user on the destination computer, a server named *srv1.contoso.com*.</span></span>

````
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a><span data-ttu-id="81c65-276">ПРИМЕР 6</span><span class="sxs-lookup"><span data-stu-id="81c65-276">EXAMPLE 6</span></span>

<span data-ttu-id="81c65-277">В этом примере всем пользователям предоставляется доступ ко всем конечным точкам на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="81c65-277">This example allows all users access to all endpoints on all computers.</span></span>
<span data-ttu-id="81c65-278">Это по сути отключает правила авторизации.</span><span class="sxs-lookup"><span data-stu-id="81c65-278">This essentially turns off authorization rules.\\</span></span>
<span data-ttu-id="81c65-279">**Примечание**. Использование подстановочного знака `*` не рекомендуется для конфиденциальных развертываний и может использоваться только в тестовых средах или развертываниях с невысокими требованиями к безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c65-279">**Note**: Use of the `*` wildcard character is not recommended for security-sensitive deployments and should only be considered for test environments or used in deployments where security can be relaxed.</span></span>

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a><span data-ttu-id="81c65-280">См. также</span><span class="sxs-lookup"><span data-stu-id="81c65-280">See Also</span></span>

- <span data-ttu-id="81c65-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="81c65-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span></span>
- <span data-ttu-id="81c65-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="81c65-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span></span>
- <span data-ttu-id="81c65-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="81c65-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span></span>
- <span data-ttu-id="81c65-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="81c65-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span></span>
- [<span data-ttu-id="81c65-285">Add-Member</span><span class="sxs-lookup"><span data-stu-id="81c65-285">Add-Member</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113280)
- [<span data-ttu-id="81c65-286">New-Object</span><span class="sxs-lookup"><span data-stu-id="81c65-286">New-Object</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113355)
- [<span data-ttu-id="81c65-287">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="81c65-287">Get-Credential</span></span>](http://go.microsoft.com/fwlink/?LinkID=293936)