---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Service в DSC
ms.openlocfilehash: 3e2db8999ab1db2964f88e1ee14c6ad6e641c5e3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-service-resource"></a><span data-ttu-id="5001a-103">Ресурс Service в DSC</span><span class="sxs-lookup"><span data-stu-id="5001a-103">DSC Service Resource</span></span>

> <span data-ttu-id="5001a-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5001a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="5001a-105">Ресурс **Service** в DSC Windows PowerShell предоставляет механизм управления службами на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="5001a-105">The **Service** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="5001a-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5001a-106">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="5001a-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="5001a-107">Properties</span></span>

|  <span data-ttu-id="5001a-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="5001a-108">Property</span></span>  |  <span data-ttu-id="5001a-109">Описание</span><span class="sxs-lookup"><span data-stu-id="5001a-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="5001a-110">Name</span><span class="sxs-lookup"><span data-stu-id="5001a-110">Name</span></span>| <span data-ttu-id="5001a-111">Указывает имя службы.</span><span class="sxs-lookup"><span data-stu-id="5001a-111">Indicates the service name.</span></span> <span data-ttu-id="5001a-112">Обратите внимание! Иногда оно отличается от отображаемого имени.</span><span class="sxs-lookup"><span data-stu-id="5001a-112">Note that sometimes this is different from the display name.</span></span> <span data-ttu-id="5001a-113">Список служб и их текущее состояние можно получить с помощью командлета Get-Service.</span><span class="sxs-lookup"><span data-stu-id="5001a-113">You can get a list of the services and their current state with the Get-Service cmdlet.</span></span>|
| <span data-ttu-id="5001a-114">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="5001a-114">BuiltInAccount</span></span>| <span data-ttu-id="5001a-115">Указывает учетную запись, используемую службой для входа.</span><span class="sxs-lookup"><span data-stu-id="5001a-115">Indicates the sign-in account to use for the service.</span></span> <span data-ttu-id="5001a-116">Допустимые значения этого свойства: **LocalService**, **LocalSystem** и **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="5001a-116">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="5001a-117">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="5001a-117">Credential</span></span>| <span data-ttu-id="5001a-118">Указывает учетные данные для учетной записи, от имени которой будет запускаться служба.</span><span class="sxs-lookup"><span data-stu-id="5001a-118">Indicates credentials for the account that the service will run under.</span></span> <span data-ttu-id="5001a-119">Это свойство нельзя использовать одновременно со свойством __BuiltinAccount__.</span><span class="sxs-lookup"><span data-stu-id="5001a-119">This property and the __BuiltinAccount__ property cannot be used together.</span></span>|
| <span data-ttu-id="5001a-120">DependsOn</span><span class="sxs-lookup"><span data-stu-id="5001a-120">DependsOn</span></span>| <span data-ttu-id="5001a-121">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="5001a-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="5001a-122">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5001a-122">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="5001a-123">StartupType</span><span class="sxs-lookup"><span data-stu-id="5001a-123">StartupType</span></span>| <span data-ttu-id="5001a-124">Указывает тип запуска службы.</span><span class="sxs-lookup"><span data-stu-id="5001a-124">Indicates the startup type for the service.</span></span> <span data-ttu-id="5001a-125">Допустимые значения этого свойства: **Automatic**, **Disabled** и **Manual**.</span><span class="sxs-lookup"><span data-stu-id="5001a-125">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="5001a-126">State</span><span class="sxs-lookup"><span data-stu-id="5001a-126">State</span></span>| <span data-ttu-id="5001a-127">Указывает состояние, в котором должна находиться служба.</span><span class="sxs-lookup"><span data-stu-id="5001a-127">Indicates the state you want to ensure for the service.</span></span>|
| <span data-ttu-id="5001a-128">Описание</span><span class="sxs-lookup"><span data-stu-id="5001a-128">Description</span></span> | <span data-ttu-id="5001a-129">Указывает описание целевой службы.</span><span class="sxs-lookup"><span data-stu-id="5001a-129">Indicates the description of the target service.</span></span>|
| <span data-ttu-id="5001a-130">DisplayName</span><span class="sxs-lookup"><span data-stu-id="5001a-130">DisplayName</span></span> | <span data-ttu-id="5001a-131">Указывает отображаемое имя целевой службы.</span><span class="sxs-lookup"><span data-stu-id="5001a-131">Indicates the display name of the target service.</span></span>|
| <span data-ttu-id="5001a-132">Ensure</span><span class="sxs-lookup"><span data-stu-id="5001a-132">Ensure</span></span> | <span data-ttu-id="5001a-133">Указывает, имеется ли целевая служба в системе.</span><span class="sxs-lookup"><span data-stu-id="5001a-133">Indicates whether the target service exists on the system.</span></span> <span data-ttu-id="5001a-134">Если целевая служба не должна существовать, укажите для этого свойства значение **Absent**.</span><span class="sxs-lookup"><span data-stu-id="5001a-134">Set this property to **Absent** to ensure that the target service does not exist.</span></span> <span data-ttu-id="5001a-135">Если целевая служба должна существовать, укажите значение **Present** (используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="5001a-135">Setting it to **Present** (the default value) ensures that target service exists.</span></span>|
| <span data-ttu-id="5001a-136">путь</span><span class="sxs-lookup"><span data-stu-id="5001a-136">Path</span></span> | <span data-ttu-id="5001a-137">Указывает путь к двоичному файлу для новой службы.</span><span class="sxs-lookup"><span data-stu-id="5001a-137">Indicates the path to the binary file for a new service.</span></span>|

## <a name="example"></a><span data-ttu-id="5001a-138">Пример</span><span class="sxs-lookup"><span data-stu-id="5001a-138">Example</span></span>

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```