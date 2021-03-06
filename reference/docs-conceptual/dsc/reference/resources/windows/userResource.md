---
ms.date: 07/16/2020
ms.topic: reference
title: Ресурс User в DSC
description: Ресурс User в DSC
ms.openlocfilehash: b14f8d434ef3e1eb220fe7b0b18a011014c9ae6c
ms.sourcegitcommit: 196c7f8cd24560cac70c88acc89909f17a86aea9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2020
ms.locfileid: "93142606"
---
# <a name="dsc-user-resource"></a>Ресурс User в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.x

Ресурс **User** в DSC Windows PowerShell предоставляет механизм управления локальными учетными записями на целевом узле.

[!INCLUDE [Updated DSC Resources](../../../../../includes/dsc-resources.md)]

## <a name="syntax"></a>Синтаксис

```Syntax
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Свойства

|Свойство |Description |
|---|---|
|UserName |Указывает имя учетной записи, для которой требуется обеспечить определенное состояние. |
|Description |Указывает описание учетной записи пользователя. |
|Выключено |Указывает, включена ли учетная запись. Присвойте этому свойству значение `$true`, чтобы отключить учетную запись, и `$false`, чтобы включить ее. |
|FullName |Представляет строку с полным именем для учетной записи пользователя. |
|Пароль |Указывает пароль для этой учетной записи. |
|PasswordChangeNotAllowed |Указывает, может ли пользователь изменить пароль. Присвойте этому свойству значение `$true`, чтобы пользователь не мог изменить пароль, и `$false`, чтобы мог. Значение по умолчанию — `$false`. |
|PasswordChangeRequired |Указывает, требуется ли смена пароля при следующем входе пользователя в систему. Присвойте этому свойству значение `$true`, если пользователь должен изменить пароль. Значение по умолчанию — `$true`. |
|PasswordNeverExpires |Указывает, может ли истечь срок действия пароля. Присвойте этому свойству значение `$true`, чтобы срок действия пароля никогда не истекал. Задайте значение `$false`, чтобы ограничить срок действия пароля. Значение по умолчанию — `$false`. |

## <a name="common-properties"></a>Общие свойства

|Свойство |Description |
|---|---|
|DependsOn |Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — ResourceType, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Указывает, существует ли учетная запись. Присвойте этому свойству значение **Present** , чтобы гарантировать, что учетная запись существует, и **Absent** в противном случае. Значение по умолчанию — **Present** . |
|PsDscRunAsCredential |Задает учетные данные для выполнения всего ресурса от другого имени. |

> [!NOTE]
> В WMF 5.0 было добавлено общее свойство **PsDscRunAsCredential** , разрешающее запуск любого ресурса DSC в контексте других учетных данных. Дополнительные сведения см. в разделе [Использование учетных данных с ресурсами DSC](../../../configurations/runasuser.md).

## <a name="example"></a>Пример

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```
