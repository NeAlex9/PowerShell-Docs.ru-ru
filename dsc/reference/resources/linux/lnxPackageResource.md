---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxPackage в DSC для Linux
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047603"
---
# <a name="dsc-for-linux-nxpackage-resource"></a>Ресурс nxPackage в DSC для Linux

Ресурс **nxPackage** в настройке требуемого состояния PowerShell предоставляет механизм управления пакетами на узле Linux.

## <a name="syntax"></a>Синтаксис

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Свойства

|  Свойство |  Описание |
|---|---|
| Name| Указывает имя пакета, для которого требуется обеспечить определенное состояние.|
| Ensure| Определяет, нужно ли проверять существование пакета. Чтобы убедиться, что пакет существует, укажите для этого свойства значение Present. Чтобы убедиться, что пакет не существует, укажите для этого свойства значение Absent. Значение по умолчанию — Present.|
| PackageManager| Поддерживаются значения yum, apt и zypper. Указывает, какой диспетчер пакетов нужно использовать при установке пакетов. Если свойство **FilePath** указано, пакет будет установлен по указанному пути. В противном случае для установки пакета будет использоваться диспетчер пакетов из предварительно настроенного репозитория. Если ни одно из свойств **PackageManager** и **FilePath** не указано, будет использоваться диспетчер пакетов, предусмотренный для системы по умолчанию.|
| FilePath| Путь к файлу пакета.|
| PackageGroup| Если свойство имеет значение **$true**, в качестве параметра **Name** должно быть задано имя группы пакетов для использования с **PackageManager**. **PackageGroup** не используется, если задано свойство **FilePath**.|
| Аргументы| Строка аргументов, которая будет передана в пакет в указанном виде.|
| ReturnCode| Ожидаемый код возврата. Если фактический код возврата не соответствует указанному здесь значению, настройка вернет ошибку.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Пример

В следующем примере с помощью диспетчера пакетов Yum проверяется, установлен ли пакет с именем httpd на компьютере Linux.

```
Import-DSCResource -Module nx

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```