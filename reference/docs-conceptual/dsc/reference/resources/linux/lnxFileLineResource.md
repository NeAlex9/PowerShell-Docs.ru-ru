---
ms.date: 09/20/2019
keywords: dsc,powershell,конфигурация,установка
title: Ресурса nxFileLine в DSC для Linux
ms.openlocfilehash: 2e94bab318b5db65df88d268a88585079bab89bf
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953221"
---
# <a name="dsc-for-linux-nxfileline-resource"></a>Ресурса nxFileLine в DSC для Linux

Ресурс **nxFileLine** в DSC PowerShell предоставляет механизм управления строками в файле конфигурации на узле Linux.

## <a name="syntax"></a>Синтаксис

```Syntax
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a>Свойства

|Свойство |Описание |
|---|---|
|FilePath |Полный путь к файлу для управления строками на целевом узле. |
|ContainsLine |Строка, которая должна существовать в файле. Если в файле эта строка отсутствует, она будет добавлена. Свойство **ContainsLine** является обязательным, но, если оно не требуется, можно задать в качестве его значения пустую строку (`ContainsLine = ""`). |
|DoesNotContainPattern |Шаблон регулярных выражений для строк, которые не должны присутствовать в файле. Присутствующие в файле строки, которые соответствуют этому регулярному выражению, будут удалены. |

## <a name="common-properties"></a>Общие свойства

|Свойство |Описание |
|---|---|
|DependsOn |Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — ResourceType, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`. |

## <a name="example"></a>Пример

В этом примере показывается, как использовать ресурс **nxFileLine** для настройки файла `/etc/sudoers`, чтобы пользователь monuser не требовал использовать телетайп (TTY).

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = "/etc/sudoers"
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```