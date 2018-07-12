---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс User в DSC
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892531"
---
# <a name="dsc-user-resource"></a><span data-ttu-id="8750b-103">Ресурс User в DSC</span><span class="sxs-lookup"><span data-stu-id="8750b-103">DSC User Resource</span></span>

<span data-ttu-id="8750b-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8750b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="8750b-105">Ресурс **User** в DSC Windows PowerShell предоставляет механизм управления локальными учетными записями на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="8750b-105">The **User** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="8750b-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="8750b-106">Syntax</span></span>

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="8750b-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="8750b-107">Properties</span></span>

|  <span data-ttu-id="8750b-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="8750b-108">Property</span></span>  |  <span data-ttu-id="8750b-109">Описание</span><span class="sxs-lookup"><span data-stu-id="8750b-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="8750b-110">UserName</span><span class="sxs-lookup"><span data-stu-id="8750b-110">UserName</span></span>| <span data-ttu-id="8750b-111">Указывает имя учетной записи, для которой требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="8750b-111">Indicates the account name for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="8750b-112">Описание</span><span class="sxs-lookup"><span data-stu-id="8750b-112">Description</span></span>| <span data-ttu-id="8750b-113">Указывает описание учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="8750b-113">Indicates the description you want to use for the user account.</span></span>|
| <span data-ttu-id="8750b-114">Отключен</span><span class="sxs-lookup"><span data-stu-id="8750b-114">Disabled</span></span>| <span data-ttu-id="8750b-115">Указывает, включена ли учетная запись.</span><span class="sxs-lookup"><span data-stu-id="8750b-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="8750b-116">Присвойте этому свойству значение `$true`, чтобы отключить учетную запись, и `$false`, чтобы включить ее.</span><span class="sxs-lookup"><span data-stu-id="8750b-116">Set this property to `$true` to ensure that this account is disabled, and set it to `$false` to ensure that it is enabled.</span></span>|
| <span data-ttu-id="8750b-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="8750b-117">Ensure</span></span>| <span data-ttu-id="8750b-118">Указывает, существует ли учетная запись.</span><span class="sxs-lookup"><span data-stu-id="8750b-118">Indicates if the account exists.</span></span> <span data-ttu-id="8750b-119">Присвойте этому свойству значение Present, если учетная запись существует, и Absent, если не существует.</span><span class="sxs-lookup"><span data-stu-id="8750b-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="8750b-120">FullName</span><span class="sxs-lookup"><span data-stu-id="8750b-120">FullName</span></span>| <span data-ttu-id="8750b-121">Представляет строку с полным именем для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="8750b-121">Represents a string with the full name you want to use for the user account.</span></span>|
| <span data-ttu-id="8750b-122">Пароль</span><span class="sxs-lookup"><span data-stu-id="8750b-122">Password</span></span>| <span data-ttu-id="8750b-123">Указывает пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8750b-123">Indicates the password you want to use for this account.</span></span> |
| <span data-ttu-id="8750b-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="8750b-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="8750b-125">Указывает, может ли пользователь изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="8750b-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="8750b-126">Присвойте этому свойству значение `$true`, чтобы пользователь не мог изменить пароль, и `$false`, чтобы мог.</span><span class="sxs-lookup"><span data-stu-id="8750b-126">Set this property to `$true` to ensure that the user cannot change the password, and set it to `$false` to allow the user to change the password.</span></span> <span data-ttu-id="8750b-127">Значение по умолчанию — `$false`.</span><span class="sxs-lookup"><span data-stu-id="8750b-127">The default value is `$false`.</span></span>|
| <span data-ttu-id="8750b-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="8750b-128">PasswordChangeRequired</span></span>| <span data-ttu-id="8750b-129">Указывает, требуется ли смена пароля при следующем входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="8750b-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="8750b-130">Присвойте этому свойству значение `$true`, если пользователь должен изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="8750b-130">Set this property to `$true` if the user must change the password.</span></span> <span data-ttu-id="8750b-131">Значение по умолчанию — `$true`.</span><span class="sxs-lookup"><span data-stu-id="8750b-131">The default value is `$true`.</span></span>|
| <span data-ttu-id="8750b-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="8750b-132">PasswordNeverExpires</span></span>| <span data-ttu-id="8750b-133">Указывает, может ли истечь срок действия пароля.</span><span class="sxs-lookup"><span data-stu-id="8750b-133">Indicates if the password will expire.</span></span> <span data-ttu-id="8750b-134">Присвойте этому свойству значение `$true`, чтобы срок действия пароля никогда не истекал, а в противном случае — значение `$false`.</span><span class="sxs-lookup"><span data-stu-id="8750b-134">To ensure that the password for this account will never expire, set this property to `$true`, and set it to `$false` if the password will expire.</span></span> <span data-ttu-id="8750b-135">Значение по умолчанию — `$false`.</span><span class="sxs-lookup"><span data-stu-id="8750b-135">The default value is `$false`.</span></span>|
| <span data-ttu-id="8750b-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="8750b-136">DependsOn</span></span> | <span data-ttu-id="8750b-137">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="8750b-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="8750b-138">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="8750b-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="8750b-139">Пример</span><span class="sxs-lookup"><span data-stu-id="8750b-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```