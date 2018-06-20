---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxEnvironment в DSC для Linux
ms.openlocfilehash: 3c9f39760e0fba7fac060f29f9e808a3a434401f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189488"
---
# <a name="dsc-for-linux-nxenvironment-resource"></a>Ресурс nxEnvironment в DSC для Linux

Ресурс **nxEnvironment** в DSC PowerShell предоставляет механизм управления системными переменными среды на узле Linux.

## <a name="syntax"></a>Синтаксис

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Свойства

|  Свойство |  Описание |
|---|---|
| Name| Указывает имя переменной среды, для которой требуется обеспечить определенное состояние.|
| Значение| Значение, которое нужно присвоить переменной среды.|
| Ensure| Определяет, нужно ли проверять существование переменной. Чтобы убедиться, что переменная существует, укажите для этого свойства значение Present. Чтобы убедиться, что переменная не существует, укажите для этого свойства значение Absent. Значение по умолчанию — Present.|
| путь| Определяет настраиваемую переменную среды. Для переменной **Path** присвойте этому свойству значение **$true**; для остальных переменных используйте значение **$false**. Значение по умолчанию — **$false**. Если настраивается переменная **Path**, к существующему значению прикрепляется значение свойства **Value**.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>Дополнительные сведения

* Если свойство **Path** не задано или имеет значение **$false**, управление переменными среды осуществляется в файле `/etc/environment`. Для доступа к управляемым переменным среды может потребоваться настроить файл `/etc/environment` в качестве источника для программ или сценариев.
* Если свойство **Path** имеет значение **$true**, управление переменными среды осуществляется в файле `/etc/profile.d/DSCenvironment.sh`. Если этот файл не существует, он будет создан. Если свойство **Ensure** имеет значение Absent, а свойство **Path** — значение **$true**, существующая переменная среды будет удалена только из файла `/etc/profile.d/DSCenvironment.sh`; остальные файлы затронуты не будут.

## <a name="example"></a>Пример

В следующем примере показано, как использовать ресурс **nxEnvironment**, чтобы убедиться, что переменная **TestEnvironmentVariable** существует и имеет значение Test-Value. Если переменная **TestEnvironmentVariable** не существует, она будет создана.

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```