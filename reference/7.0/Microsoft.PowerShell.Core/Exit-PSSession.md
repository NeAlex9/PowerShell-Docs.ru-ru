---
external help file: System.Management.Automation.dll-Help.xml
keywords: powershell,командлет
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/exit-pssession?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Exit-PSSession;
ms.openlocfilehash: fb6c0f930536e7a32d83c9f390a0e351a6952550
ms.sourcegitcommit: 2e497178126b2b33a169ff04c31e251e0b59e89b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2020
ms.locfileid: "93209241"
---
# Exit-PSSession;

## Краткий обзор
Завершает интерактивный сеанс с удаленным компьютером.

## SYNTAX

```
Exit-PSSession [<CommonParameters>]
```

## DESCRIPTION

Командлет **Exit-PSSession** завершает интерактивные сеансы, запущенные с помощью командлета Enter-PSSession.

Можно также использовать ключевое слово **Exit** для завершения интерактивного сеанса.
Результат такой же, как и при использовании **Exit-PSSession** .

## Примеры

### Пример 1. Запуск и завершение интерактивного сеанса

```
PS> Enter-PSSession -computername Server01
Server01\PS> Exit-PSSession
PS>
```

Эти команды создают и затем завершают интерактивный сеанс с удаленным компьютером Server01.

### Пример 2. Запуск и завершение интерактивного сеанса с помощью объекта PSSession

```
PS> $s = New-PSSession -ComputerName Server01
PS> Enter-PSSession -Session $s
Server01\PS> Exit-PSSession
PS> $s
Id Name            ComputerName    State    ConfigurationName
-- ----            ------------    -----    -----------------
1  Session1        Server01        Opened   Microsoft.PowerShell
```

Эти команды запускают и останавливают интерактивный сеанс с компьютером Server01, использующим сеанс PowerShell ( **PSSession** ).

Поскольку интерактивный сеанс запущен с помощью сеанса PowerShell, сеанс **PSSession** по-прежнему доступен по окончании интерактивного сеанса.
Если используется параметр *ComputerName* , команда **Enter-PSSession** создает временный сеанс, который закрывается по завершении интерактивного сеанса.

Первая команда использует командлет New-PSSession для создания **сеанса PSSession** на компьютере Server01.
Команда сохраняет **PSSession** в переменной $s.

Вторая команда использует **Enter-PSSession** для запуска интерактивного сеанса с использованием сеанса **PSSession** в $s.

Третья команда использует **Exit-PSSession** для прекращения интерактивного сеанса.

Последняя команда отображает **PSSession** в переменной $s.
Свойство **State** показывает, что **сеанс PSSession** по-прежнему открыт и доступен для использования.

### Пример 3. Использование ключевого слова Exit для завершения сеанса

```
PS> Enter-PSSession -computername Server01
Server01\PS> exit
PS>
```

В этом примере используется ключевое слово **Exit** для завершения интерактивного сеанса, запущенного с помощью команды **Enter-PSSession** .
Ключевое слово **Exit** имеет тот же результат, что и при использовании **Exit-PSSession** .

## PARAMETERS

### Общие параметры

Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable. См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Входные данные

### Нет

Нельзя передать объекты в этот командлет с помощью конвейера.

## Выходные данные

### Нет

Этот командлет не возвращает никакие выходные данные.

## ПРИМЕЧАНИЯ

* Этот командлет принимает только общие параметры.

*

## Связанные ссылки

[Connect-PSSession](Connect-PSSession.md)

[Disconnect-PSSession](Disconnect-PSSession.md)

[Enter-PSSession](Enter-PSSession.md)

[Get-PSSession](Get-PSSession.md)

[Invoke-Command](Invoke-Command.md)

[New-PSSession](New-PSSession.md)

[Receive-PSSession](Receive-PSSession.md)

[Remove-PSSession](Remove-PSSession.md)