---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxScript в DSC для Linux
ms.openlocfilehash: 339968512ab1c16c4c3785a3a19b00c3fbbf9ea1
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047588"
---
# <a name="dsc-for-linux-nxscript-resource"></a>Ресурс nxScript в DSC для Linux

Ресурс **nxScript** в DSC PowerShell предоставляет механизм управления сценариями Linux на узле Linux.

## <a name="syntax"></a>Синтаксис

```
nxScript <string> #ResourceName
{
    GetScript = <string>
    SetScript = <string>
    TestScript = <string>
    [ User = <string> ]
    [ Group = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Свойства

|  Свойство |  Описание |
|---|---|
| GetScript| Предоставляет сценарий, который выполняется при вызове командлета [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx). Сценарий должен начинаться со знака решетки, например #!/bin/bash.|
| SetScript| Предоставляет сценарий. При вызове командлета [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) в первую очередь выполняется команда **TestScript**. Если блок **TestScript** возвращает код выхода, отличный от 0, запускается блок **SetScript**. Если блок **TestScript** возвращает код выхода 0, **SetScript** не выполняется. Сценарий должен начинаться со знака решетки, например `#!/bin/bash`.|
| TestScript| Предоставляет сценарий. При вызове командлета [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) выполняется этот сценарий. Если он возвращает код выхода, отличный от 0, выполняется команда SetScript. Если он возвращает код выхода 0, команда **SetScript** не выполняется. Кроме того, **TestScript** выполняется при вызове командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx). Однако в этом случае **SetScript** не будет запущен, какое бы значение ни вернул блок **TestScript**. Блок **TestScript** должен возвращать код выхода 0, если фактическая конфигурация соответствует текущей настройке требуемого состояния, и другой код выхода, если они не совпадают. (Текущей настройкой требуемого состояния является последняя конфигурация, активированная на узле, который использует DSC.) Сценарий должен начинаться со знака решетки, например 1#!/bin/bash.1|
| User| Указывает, от имени какого пользователя выполняется сценарий.|
| Группа| Указывает, от имени какой группы выполняется сценарий.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Пример

В следующем примере показано применение ресурса **nxScript** для дополнительного управления конфигурацией.

```
Import-DSCResource -Module nx

Node $node {
nxScript KeepDirEmpty{

    GetScript = @"
#!/bin/bash
ls /tmp/mydir/ | wc -l
"@

    SetScript = @"
#!/bin/bash
rm -rf /tmp/mydir/*
"@

    TestScript = @'
#!/bin/bash
filecount=`ls /tmp/mydir | wc -l`
if [ $filecount -gt 0 ]
then
    exit 1
else
    exit 0
fi
'@
}
}
```