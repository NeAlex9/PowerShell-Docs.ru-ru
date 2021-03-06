---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
keywords: powershell,командлет
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 10/14/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/write-debug?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Write-Debug
ms.openlocfilehash: 7e622367f1753fc15bed26fe083e9f343fd82b85
ms.sourcegitcommit: 16883bb67e34b3915798070f60f974bf85160bd3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2020
ms.locfileid: "93232838"
---
# Write-Debug

## Краткий обзор
Выводит сообщение отладки на консоль.

## SYNTAX

```
Write-Debug [-Message] <String> [<CommonParameters>]
```

## DESCRIPTION

`Write-Debug`Командлет записывает сообщения отладки на узел из скрипта или команды.

По умолчанию сообщения отладки не отображаются в консоли, но их можно отобразить с помощью параметра **отладки** или `$DebugPreference` переменной.

## Примеры

### Пример 1. понимание $DebugPreference

В этом примере записывается сообщение отладки.

```powershell
Write-Debug "Cannot open file."
```

Значение по умолчанию `$DebugPreference` — **SilentlyContinue**. Поэтому сообщение не отображается в консоли.

### Пример 2. изменение значения $DebugPreference

В этом примере показан результат изменения значения `$DebugPreference` переменной. Сначала мы отображаем текущее значение `$DebugPreference` и попытались написать сообщение отладки. Затем мы изменим значение `$DebugPreference` на **Continue** , что позволяет отображать сообщения отладки.

```
PS> $DebugPreference
SilentlyContinue
PS> Write-Debug "Cannot open file."
PS>
PS> $DebugPreference = "Continue"
PS> Write-Debug "Cannot open file."
DEBUG: Cannot open file.
```

Дополнительные сведения о `$DebugPreference` см. в разделе [about_Preference_Variables](/powershell/module/Microsoft.PowerShell.Core/About/about_Preference_Variables).

### Пример 3. Переопределение $DebugPreference с помощью параметра Debug

`Test-Debug`Функция записывает значение `$DebugPreference` переменной в узел PowerShell и в поток отладки. В этом примере мы используем параметр **Debug** для переопределения `$DebugPreference` значения.

```powershell
function Test-Debug {
    [CmdletBinding()]
    param()
    Write-Debug ('$DebugPreference is ' + $DebugPreference)
    Write-Host ('$DebugPreference is ' + $DebugPreference)
}
```

```
PS> Test-Debug
$DebugPreference is SilentlyContinue

PS> Test-Debug -Debug
DEBUG: $DebugPreference is Inquire

Confirm
Continue with this operation?
[Y] Yes  [A] Yes to All  [H] Halt Command  [?] Help (default is "Y"):
$DebugPreference is Inquire
PS> $DebugPreference
SilentlyContinue
```

Обратите внимание, что `$DebugPreference` при использовании параметра **Debug** значение изменяется. Это изменение влияет только на область действия функции. Это значение не затрагивается за пределами функции.

> [!NOTE]
> Если значение параметра `$DebugPreference` является **запросом** , PowerShell останавливает выполнение, чтобы задать продолжение выполнения.

Дополнительные сведения об общем параметре **Debug** см. в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## PARAMETERS

### -Message

Задает сообщение отладки для отправки на консоль.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: Msg

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### Общие параметры

Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable. См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Входные данные

### System.String

Строку, содержащую сообщение отладки, можно передать в `Write-Debug` .

## Выходные данные

### Нет

`Write-Debug` выполняет запись только в поток отладки. Он не записывает никакие объекты в конвейер.

## ПРИМЕЧАНИЯ

## Связанные ссылки

[about_Output_Streams](../Microsoft.PowerShell.Core/About/about_Output_Streams.md)

[about_Redirection](../Microsoft.PowerShell.Core/About/about_Redirection.md)

[Ошибка записи](Write-Error.md)

[Write-Host](Write-Host.md)

[Write-Output](Write-Output.md)

[Write-Progress](Write-Progress.md)

[Write-Verbose](Write-Verbose.md)

[Write-Warning](Write-Warning.md)
