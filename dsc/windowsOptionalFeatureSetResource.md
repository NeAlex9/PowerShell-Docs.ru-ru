---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс DSC WindowsOptionalFeatureSet
ms.openlocfilehash: 7c5eb553b396776f54a36bec8971f71ec61f9354
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187663"
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a>Ресурс DSC WindowsOptionalFeatureSet

> Область применения: Windows PowerShell 5.0

Ресурс **WindowsOptionalFeatureSet** в DSC Windows PowerShell предоставляет механизм включения дополнительных компонентов на целевом узле.
Он является [составным ресурсом](authoringResourceComposite.md), который вызывает [ресурс WindowsOptionalFeature](windowsOptionalFeatureResource.md) для каждого компонента, указанного в свойстве `Name`.

Используйте этот ресурс, если нужно настроить одинаковое состояние для нескольких дополнительных компонентов Windows.

## <a name="syntax"></a>Синтаксис

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   |
|---|---|
| Name| Указывает имена компонентов, которые необходимо включить или отключить.|
| Ensure| Указывает, включены ли компоненты. Чтобы включить компоненты, установите для этого свойства значение "Включить", чтобы отключить — значение "Отключить".|
| Источник| Не реализовано.|
| NoWindowsUpdateCheck| Указывает, обращается ли система DISM к Центру обновления Windows при поиске исходных файлов для включения компонентов. Если задано значение $true, система DISM не обращается к Центру обновления Windows.|
| RemoveFilesOnDisable| Задайте значение **$true**, чтобы удалить все файлы, связанные с компонентами, при их отключении (то есть когда свойству **Ensure** присваивается значение Absent).|
| Уровень журнала| Максимальный уровень результатов, показываемый в журналах. Допустимые значения: ErrorsOnly (в журналы записываются только ошибки), ErrorsAndWarning (в журналы записываются ошибки и предупреждения) и ErrorsAndWarningAndInformation (в журналы записываются ошибки, предупреждения и отладочные сведения).|
| LogPath| Путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.|
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|