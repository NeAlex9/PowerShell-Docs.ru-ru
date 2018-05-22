---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Package в DSC
ms.openlocfilehash: 16f7f1b8fa7b84bcfdeb09fdc46db9c93113e70c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-package-resource"></a>Ресурс Package в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **Package** в DSC Windows PowerShell предоставляет механизм установки или удаления пакетов, таких как пакеты установщика Windows и setup.exe, на целевом узле.

## <a name="syntax"></a>Синтаксис

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   |
|---|---|
| Name| Указывает имя пакета, для которого требуется обеспечить определенное состояние.|
| путь| Указывает путь к файлу пакета.|
| ProductID| Указывает уникальный идентификатор пакета.|
| Аргументы| Указывает строку аргументов, которая будет передана в пакет в указанном виде.|
| Учетные данные| Предоставляет доступ к пакету в удаленном источнике. Это свойство не используется для установки пакета. Пакет всегда устанавливается в локальной системе.|
| Ensure| Указывает, установлен ли пакет. Если это свойство имеет значение Absent, пакет не устанавливается (а если он уже установлен, то удаляется). Если это свойство имеет значение Present (по умолчанию), пакет устанавливается.|
| LogPath| Указывает полный путь к папке, где нужно сохранить файл журнала для установки или удаления пакета.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: "DependsOn = "[ResourceType]ResourceName"".|
| ReturnCode| Указывает ожидаемый код возврата. Если фактический код возврата не соответствует указанному здесь значению, настройка вернет ошибку.|

## <a name="example"></a>Пример

В этом примере выполняется установщик MSI, который находится по указанному пути и имеет указанный идентификатор.

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    }
}
```