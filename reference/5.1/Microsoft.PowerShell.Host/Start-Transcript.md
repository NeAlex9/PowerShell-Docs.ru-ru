---
external help file: Microsoft.PowerShell.ConsoleHost.dll-help.xml
keywords: powershell,командлет
Locale: en-US
Module Name: Microsoft.PowerShell.Host
ms.date: 04/22/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.host/start-transcript?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Start-Transcript
ms.openlocfilehash: c7e95988c385a32802c93f92216710746d268e5e
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2020
ms.locfileid: "93226634"
---
# Start-Transcript

## Краткий обзор
Создает запись для всего сеанса PowerShell или его части в текстовый файл.

## SYNTAX

### ByPath (по умолчанию)

```
Start-Transcript [[-Path] <String>] [-Append] [-Force] [-NoClobber] [-IncludeInvocationHeader] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

### ByLiteralPath

```
Start-Transcript [[-LiteralPath] <String>] [-Append] [-Force] [-NoClobber] [-IncludeInvocationHeader] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

### бйоутпутдиректори

```
Start-Transcript [[-OutputDirectory] <String>] [-Append] [-Force] [-NoClobber] [-IncludeInvocationHeader]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

`Start-Transcript`Командлет создает запись или часть сеанса PowerShell в текстовый файл. Запись включает в себя все команды, вводимые пользователем, и все выходные данные, выводимые в консоли.

Начиная с Windows PowerShell 5,0, `Start-Transcript` содержит имя узла в созданном файле для всех записей. Это особенно полезно, если ведение журнала предприятия является централизованным.
Файлы, создаваемые `Start-Transcript` командлетом, содержат случайные символы в именах, чтобы предотвратить возможную перезапись или дублирование при одновременном запуске двух или более записей.
Это также предотвращает несанкционированный Поиск записей, хранящихся в централизованном файловом ресурсе.

## Примеры

### Пример 1. Запуск файла транскрипции с параметрами по умолчанию

```powershell
Start-Transcript
```

Эта команда начинает записывать сеанс в файл в папке по умолчанию.

### Пример 2. Запуск файла транскрипции в указанном расположении

```powershell
Start-Transcript -Path "C:\transcripts\transcript0.txt" -NoClobber
```

Эта команда запускает запись в `Transcript0.txt` файле в `C:\transcripts` . Так как используется параметр **NoClobber** , команда предотвращает перезапись существующих файлов. Если `Transcript0.txt` файл уже существует, команда завершается ошибкой.

## PARAMETERS

### — Добавление

Указывает, что этот командлет добавляет новую запись в конец существующего файла. Используйте параметр **path** , чтобы указать файл.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Позволяет командлету добавить запись к существующему файлу, доступному только для чтения. При использовании применительно к файлу, доступному только для чтения, этот командлет изменяет разрешения файла, делая его доступным для чтения и записи. Командлет не может переопределить ограничения безопасности при использовании этого параметра.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Инклудеинвокатионхеадер

Указывает, что этот командлет регистрирует метку времени при выполнении команд.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LiteralPath

Задает расположение файла транскрипции. В отличие от параметра **Path** значение параметра **LiteralPath** используется в точности так, как вводится. Никакие символы не интерпретируются как знаки подстановки. Если путь содержит escape-символы, заключите его в одинарные кавычки. Одинарные кавычки сообщают PowerShell не интерпретировать какие-либо символы как escape-последовательности.

```yaml
Type: System.String
Parameter Sets: ByLiteralPath
Aliases: PSPath

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoClobber

Указывает, что этот командлет не будет перезаписывать существующий файл. По умолчанию, если файл транскрипции существует по указанному пути, `Start-Transcript` перезаписывает файл без предупреждения.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: NoOverwrite

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OutputDirectory

Указывает конкретный путь и папку для сохранения записи. PowerShell автоматически назначает имя транскрипции.

```yaml
Type: System.String
Parameter Sets: ByOutputDirectory
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Задает расположение файла транскрипции. Введите путь к `.txt` файлу. Использовать подстановочные знаки запрещено.

Если путь не указан, `Start-Transcript` использует путь в значении `$Transcript` глобальной переменной. Если эта переменная не создана, сохраняет записи `Start-Transcript` в `$Home\My Documents directory as \PowerShell_transcript.<time-stamp>.txt` файлах.

Если какие-либо каталоги, указанные в пути, отсутствуют, команда завершается сбоем.

```yaml
Type: System.String
Parameter Sets: ByPath
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm

Запрос подтверждения перед выполнением командлета.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Показывает, что произойдет при запуске командлета.
Командлет не выполняется.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### Общие параметры

Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable. См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Входные данные

### Нет

Нельзя передать объекты в этот командлет с помощью конвейера.

## Выходные данные

### System.String

Этот командлет возвращает строку, содержащую сообщение подтверждения и путь к выходному файлу.

## ПРИМЕЧАНИЯ

Чтобы отключить запись разговора, используйте `Stop-Transcript` командлет.

Чтобы записать весь сеанс, добавьте `Start-Transcript` команду в профиль. Дополнительные сведения см. в разделе [about_Profiles](../Microsoft.PowerShell.Core/About/about_Profiles.md).

## Связанные ссылки

[Stop-Transcript](Stop-Transcript.md)