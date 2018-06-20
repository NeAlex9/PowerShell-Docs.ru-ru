---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxSshAuthorizedKeys в DSC для Linux
ms.openlocfilehash: d4cdb727a94a5e89e8401769f24977d49bcf4929
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222043"
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a><span data-ttu-id="3bdb9-103">Ресурс nxSshAuthorizedKeys в DSC для Linux</span><span class="sxs-lookup"><span data-stu-id="3bdb9-103">DSC for Linux nxSshAuthorizedKeys Resource</span></span>

<span data-ttu-id="3bdb9-104">Ресурс **NxAuthorizedKeys** в DSC PowerShell обеспечивает механизм управления авторизованными SSH-ключами для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-104">The **nxAuthorizedKeys** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage authorized ssh keys for a specified user.</span></span>

## <a name="syntax"></a><span data-ttu-id="3bdb9-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="3bdb9-105">Syntax</span></span>

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="3bdb9-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="3bdb9-106">Properties</span></span>

|  <span data-ttu-id="3bdb9-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="3bdb9-107">Property</span></span> |  <span data-ttu-id="3bdb9-108">Описание</span><span class="sxs-lookup"><span data-stu-id="3bdb9-108">Description</span></span> |
|---|---|
| <span data-ttu-id="3bdb9-109">KeyComment</span><span class="sxs-lookup"><span data-stu-id="3bdb9-109">KeyComment</span></span>| <span data-ttu-id="3bdb9-110">Уникальный комментарий к ключу.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-110">A unique comment for the key.</span></span> <span data-ttu-id="3bdb9-111">Используется для уникальной идентификации ключей.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-111">This is used to uniquely identify keys.</span></span>|
| <span data-ttu-id="3bdb9-112">Ensure</span><span class="sxs-lookup"><span data-stu-id="3bdb9-112">Ensure</span></span>| <span data-ttu-id="3bdb9-113">Указывает, определен ли ключ.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-113">Specifies whether the key is defined.</span></span> <span data-ttu-id="3bdb9-114">Если это свойство имеет значение Absent, обеспечивается отсутствие ключа в файле авторизованных ключей пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-114">Set this property to "Absent" to ensure the key does not exist in the user’s authorized keys file.</span></span> <span data-ttu-id="3bdb9-115">Если это свойство имеет значение Present, обеспечивается наличие определения ключа в файле авторизованных ключей пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-115">Set it to "Present" to ensure the key is defined in the user’s authorized key file.</span></span>|
| <span data-ttu-id="3bdb9-116">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3bdb9-116">Username</span></span>| <span data-ttu-id="3bdb9-117">Указывает, для какого пользователя осуществляется управление авторизованными SSH-ключами.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-117">The username to manage ssh authorized keys for.</span></span> <span data-ttu-id="3bdb9-118">Если свойство не определено, пользователь по умолчанию — root.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-118">If not defined, the default user is "root".</span></span>|
| <span data-ttu-id="3bdb9-119">Клавиши</span><span class="sxs-lookup"><span data-stu-id="3bdb9-119">Key</span></span>| <span data-ttu-id="3bdb9-120">Указывает содержимое ключа</span><span class="sxs-lookup"><span data-stu-id="3bdb9-120">The contents of the key.</span></span> <span data-ttu-id="3bdb9-121">Требуется, если свойство **Ensure** имеет значение Present.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-121">This is required if **Ensure** is set to "Present".</span></span>|
| <span data-ttu-id="3bdb9-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="3bdb9-122">DependsOn</span></span> | <span data-ttu-id="3bdb9-123">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="3bdb9-124">Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="3bdb9-125">Пример</span><span class="sxs-lookup"><span data-stu-id="3bdb9-125">Example</span></span>

<span data-ttu-id="3bdb9-126">В следующем примере определяется общедоступный авторизованный SSH-ключ для пользователя monuser.</span><span class="sxs-lookup"><span data-stu-id="3bdb9-126">The following example defines a public ssh authorized key for the user "monuser".</span></span>

```
Import-DSCResource -Module nx

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
}
}
```