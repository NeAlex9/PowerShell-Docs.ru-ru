---
external help file: System.Management.Automation.dll-Help.xml
keywords: powershell,командлет
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/out-null?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Out-Null
ms.openlocfilehash: 501c0482270a5a4919ed33844beb838e231f8636
ms.sourcegitcommit: de63e9481cf8024883060aae61fb02c59c2de662
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2020
ms.locfileid: "93225985"
---
# Out-Null

## Краткий обзор
Скрывает выходные данные вместо отправки их в конвейер или отображения.

## SYNTAX

```
Out-Null [-InputObject <PSObject>] [<CommonParameters>]
```

## DESCRIPTION

Командлет **out-NULL** отправляет свои выходные данные в значение null, фактически удаляя его из конвейера и предотвращая Отображение выходных данных на экране.

## Примеры

### Пример 1. Удаление выходных данных

```powershell
Get-ChildItem | Out-Null
```

Эта команда возвращает элементы в текущем расположении или каталоге, но выходные данные не передаются через конвейер и не отображаются в командной строке.
Это полезно для скрытия выходных данных, которые не нужны.

## PARAMETERS

### -InputObject

Указывает объект, который будет отправлен в NULL (удален из конвейера).
Введите переменную, которая содержит объекты, или команду или выражение, которое возвращает объекты.

```yaml
Type: System.Management.Automation.PSObject
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### Общие параметры

Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable. См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Входные данные

### System.Management.Automation.PSObject

В этот командлет можно передать по конвейеру любой объект.

## Выходные данные

### Нет

Этот командлет не формирует никаких выходных данных.

## ПРИМЕЧАНИЯ

* Командлеты, которые содержат команду **out** (командлеты **out** ), не имеют параметров для имен или путей к файлам. Чтобы отправить данные в командлет **out** , используйте оператор конвейера (|), чтобы отправить выходные данные команды PowerShell в командлет. Также можно сохранить данные в переменную передать их в командлет с помощью параметра *InputObject*. Дополнительные сведения см. в примерах.
* **Out-NULL** не возвращает никаких выходных объектов. При передаче выходных данных **out-NULL** в командлет Get-Member, **Get-Member** сообщает о том, что объекты не указаны.

## Связанные ссылки

[Out-Default;](Out-Default.md)

[Out-Host](Out-Host.md)
