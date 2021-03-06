---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
keywords: powershell,командлет
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 5/14/2019
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.management/set-content?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Set-Content
ms.openlocfilehash: 897029cab790487f6834d021bfc447060fd39812
ms.sourcegitcommit: 9b28fb9a3d72655bb63f62af18b3a5af6a05cd3f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/07/2020
ms.locfileid: "93227901"
---
# Set-Content

## Краткий обзор
Записывает новое содержимое или заменяет существующее содержимое в файле.

## SYNTAX

### Путь (по умолчанию)

```
Set-Content [-Path] <string[]> [-Value] <Object[]> [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Force] [-Credential <pscredential>] [-WhatIf]
 [-Confirm] [-UseTransaction] [-NoNewline] [-Encoding <FileSystemCmdletProviderEncoding>]
 [-Stream <string>] [<CommonParameters>]
```

### LiteralPath

```
Set-Content [-Value] <Object[]> -LiteralPath <string[]> [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Force] [-Credential <pscredential>] [-WhatIf]
 [-Confirm] [-UseTransaction] [-NoNewline] [-Encoding <FileSystemCmdletProviderEncoding>]
 [-Stream <string>] [<CommonParameters>]
```

## DESCRIPTION

`Set-Content` — Это командлет обработки строк, который записывает новое содержимое или заменяет содержимое в файле. `Set-Content` Заменяет существующее содержимое и отличается от `Add-Content` командлета, который добавляет содержимое в файл. Чтобы отправить содержимое в `Set-Content` , можно использовать параметр **value** в командной строке или отправить содержимое через конвейер.

Если необходимо создать файлы или каталоги для следующих примеров, см. раздел [New-Item](New-Item.md).

## Примеры

### Пример 1. Замена содержимого нескольких файлов в каталоге

Этот пример заменяет содержимое для нескольких файлов в текущем каталоге.

```powershell
Get-ChildItem -Path .\Test*.txt
```

```Output
Test1.txt
Test2.txt
Test3.txt
```

```powershell
Set-Content -Path .\Test*.txt -Value 'Hello, World'
Get-Content -Path .\Test*.txt
```

```Output
Hello, World
Hello, World
Hello, World
```

`Get-ChildItem`Командлет использует параметр **path** для вывода файлов **. txt** , начинающихся с `Test*` в текущем каталоге. `Set-Content`Командлет использует параметр **path** для указания `Test*.txt` файлов. Параметр **value** предоставляет текстовую строку **Hello, World** , заменяющую существующее содержимое в каждом файле. `Get-Content`Командлет использует параметр **path** для указания `Test*.txt` файлов и отображает содержимое каждого файла в консоли PowerShell.

### Пример 2. Создание нового файла и запись содержимого

В этом примере создается новый файл и записывается текущая дата и время в файл.

```powershell
Set-Content -Path .\DateTime.txt -Value (Get-Date)
Get-Content -Path .\DateTime.txt
```

```Output
1/30/2019 09:55:08
```

`Set-Content` использует параметры **path** и **value** для создания нового файла с именем **DateTime.txt** в текущем каталоге. Параметр **value** используется `Get-Date` для получения текущих даты и времени.
`Set-Content` Записывает объект **DateTime** в файл в виде строки. `Get-Content`Командлет использует параметр **path** для вывода содержимого **DateTime.txt** в консоли PowerShell.

### Пример 3. Замена текста в файле

Эта команда заменяет все экземпляры Word в существующем файле.

```powershell
Get-Content -Path .\Notice.txt
```

```Output
Warning
Replace Warning with a new word.
The word Warning was replaced.
```

```powershell
(Get-Content -Path .\Notice.txt) |
    ForEach-Object {$_ -Replace 'Warning', 'Caution'} |
        Set-Content -Path .\Notice.txt
Get-Content -Path .\Notice.txt
```

```Output
Caution
Replace Caution with a new word.
The word Caution was replaced.
```

`Get-Content`Командлет использует параметр **path** для указания файла **Notice.txt** в текущем каталоге. `Get-Content`Команда заключена в круглые скобки, чтобы команда закончится перед отправкой конвейера.

Содержимое файла **Notice.txt** отправляется в командлет по конвейеру `ForEach-Object` .
`ForEach-Object` использует автоматическую переменную `$_` и заменяет каждое вхождение **предупреждения** с **осторожностью** . Объекты отправляются по конвейеру в `Set-Content` командлет. `Set-Content` использует параметр **path** для указания файла **Notice.txt** и записи обновленного содержимого в файл.

Последний `Get-Content` командлет отображает обновленное содержимое файла в консоли PowerShell.

### Пример 4. Использование фильтров с Set-Content

Можно указать фильтр для `Set-Content` командлета. При использовании фильтров для уточнения параметра **path** необходимо включить конечную звездочку ( `*` ), чтобы указать содержимое пути.

Следующая команда задает для содержимого всех `*.txt` файлов в `C:\Temp` каталоге пустое **значение** .

```powershell
Set-Content -Path C:\Temp\* -Filter *.txt -Value "Empty"
```

## PARAMETERS

### -Credential

> [!NOTE]
> Этот параметр не поддерживается какими-либо поставщиками, установленными с помощью PowerShell.
> Чтобы выполнить олицетворение другого пользователя или повысить свои учетные данные при выполнении этого командлета, используйте [команду Invoke-Command](../Microsoft.PowerShell.Core/Invoke-Command.md).

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Encoding

Указывает тип кодировки для целевого файла. Значение по умолчанию — `Default`.

Кодирование — это динамический параметр, к которому добавляется поставщик FileSystem `Set-Content` . Этот параметр работает только на дисках с файловой системой.

Для этого параметра допустимы следующие значения:

- `Ascii` Использует кодировку ASCII (7-разрядных).
- `BigEndianUnicode` Использует UTF-16 с обратным порядком байтов.
- `BigEndianUTF32` Использует UTF-32 с обратным порядком байтов.
- `Byte` Кодирует набор символов в последовательность байтов.
- `Default` Использует кодировку, соответствующую активной кодовой странице системы (обычно ANSI).
- `Oem` Использует кодировку, соответствующую текущей кодовой странице OEM системы.
- `String` аналогичен `Unicode`.
- `Unicode` Использует UTF-16 с прямым порядком байтов.
- `Unknown` аналогичен `Unicode`.
- `UTF7` Использует UTF-7.
- `UTF8` Использует UTF-8.
- `UTF32` Использует UTF-32 с прямым порядком байтов.

Кодирование — это динамический параметр, к которому добавляется поставщик FileSystem `Set-Content` . Этот параметр работает только на дисках с файловой системой.

```yaml
Type: Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding
Parameter Sets: (All)
Aliases:
Accepted values: ASCII, BigEndianUnicode, BigEndianUTF32, Byte, Default, OEM, String, Unicode, Unknown, UTF7, UTF8, UTF32

Required: False
Position: Named
Default value: Default
Accept pipeline input: False
Accept wildcard characters: False
```

### -Exclude

Указывает в виде массива строк элемент или элементы, которые этот командлет исключает в операции. Значение этого параметра определяет параметр **Path** . Введите элемент пути или шаблон, например `*.txt` . Можно использовать подстановочные знаки. Параметр **Exclude** эффективен, только если команда включает содержимое элемента, например `C:\Windows\*` , где подстановочный знак указывает содержимое `C:\Windows` каталога.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Filter

Задает фильтр для уточнения параметра **пути** . Поставщик [FileSystem](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md) является единственным установленным поставщиком PowerShell, поддерживающим использование фильтров. Синтаксис для языка фильтра **файловой** системы можно найти в [about_Wildcards](../Microsoft.PowerShell.Core/About/about_Wildcards.md).
Фильтры более эффективны, чем другие параметры, так как поставщик применяет их, когда командлет получает объекты, а не использует фильтры PowerShell для объектов после их извлечения.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Force

Заставляет командлет задать содержимое файла, даже если он доступен только для чтения. Применение этого параметра зависит от конкретного поставщика. Дополнительные сведения см. в разделе [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).
Параметр **Force** не переопределяет ограничения безопасности.

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

### -Include

Указывает в виде массива строк элемент или элементы, которые этот командлет включает в операцию. Значение этого параметра определяет параметр **Path** . Введите элемент пути или шаблон, например `"*.txt"` . Можно использовать подстановочные знаки. Параметр **include** действует только в том случае, если команда включает содержимое элемента, например `C:\Windows\*` , где подстановочный знак указывает содержимое `C:\Windows` каталога.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -LiteralPath

Указывает путь к одному или нескольким расположениям. Значение **LiteralPath** используется точно так же, как оно введено. Никакие символы не интерпретируются как знаки подстановки. Если путь содержит escape-символы, заключите его в одинарные кавычки. Одинарные кавычки указывают PowerShell не интерпретировать какие-либо символы как escape-последовательности.

Дополнительные сведения см. в разделе [about_Quoting_Rules](../Microsoft.Powershell.Core/About/about_Quoting_Rules.md).

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Новая строка

Строковые представления входных объектов сцепляются для формирования выходных данных. Между выходными строками не вставляются пробелы и символы новой строки. После последней выходной строки не добавляется новая строка.

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

### -PassThru

Возвращает объект, представляющий содержимое. По умолчанию этот командлет не создает выходные данные.

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

### -Path

Указывает путь к элементу, который получает содержимое.
Можно использовать подстановочные знаки.

```yaml
Type: System.String[]
Parameter Sets: Path
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -Stream

Указывает альтернативный поток данных для содержимого. Если поток не существует, этот командлет создаст его. Подстановочные знаки не поддерживаются.

**Stream** — это динамический параметр, к которому добавляется поставщик **FileSystem** `Set-Content` . Этот параметр работает только на дисках с файловой системой.

`Set-Content`С помощью командлета можно изменить содержимое **зоны.** альтернативный поток данных идентификатора. Однако не рекомендуется использовать этот способ для устранения проверок безопасности, блокирующих файлы, загружаемые из Интернета. Если вы убедитесь, что скачанный файл является надежным, используйте `Unblock-File` командлет.

Этот параметр появился в PowerShell 3,0.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseTransaction

Включает команду в активную транзакцию. Этот параметр доступен только при выполнении транзакции. Дополнительные сведения см. в разделе [about_Transactions](../Microsoft.PowerShell.Core/About/about_Transactions.md).

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: usetx

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value

Указывает новое содержимое для элемента.

```yaml
Type: System.Object[]
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
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

Показывает, что произойдет при запуске командлета. Командлет не выполняется.

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

Этот командлет поддерживает общие параметры: `-Debug` , `-ErrorAction` , `-ErrorVariable` , `-InformationAction` , `-InformationVariable` , `-OutVariable` , `-OutBuffer` , `-PipelineVariable` , `-Verbose` , `-WarningAction` и `-WarningVariable` .
См. сведения в разделе [about_CommonParameters](../Microsoft.PowerShell.Core/About/about_CommonParameters.md).

## Входные данные

### System.Object

Объект, содержащий новое значение для элемента, можно передать по конвейеру `Set-Content` .

## Выходные данные

### Нет или System.String

При использовании параметра **PassThru** `Set-Content` создает объект **System. String** , представляющий содержимое. В противном случае командлет не формирует никаких выходных данных.

## ПРИМЕЧАНИЯ

- Также можно ссылаться `Set-Content` по встроенному псевдониму `sc` .
  Дополнительные сведения см. в разделе [about_Aliases](../Microsoft.PowerShell.Core/About/about_Aliases.md).
- `Set-Content` предназначен для обработки строк. При передаче нестроковых объектов в `Set-Content` объект преобразуется в строку перед записью. Для записи объектов в файлы используйте `Out-File` .
- `Set-Content`Командлет предназначен для работы с данными, предоставляемыми любым поставщиком. Чтобы вывести список поставщиков, доступных в данном сеансе, введите командлет `Get-PsProvider`. Дополнительные сведения см. в разделе [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

## Связанные ссылки

[about_Aliases](../Microsoft.PowerShell.Core/About/about_Aliases.md)

[about_Automatic_Variables. md](../Microsoft.PowerShell.Core/About/about_Automatic_Variables.md)

[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md)

[about_Transactions](../Microsoft.PowerShell.Core/About/about_Transactions.md)

[Add-Content](Add-Content.md)

[Clear-Content](Clear-Content.md)

[Get-ChildItem](Get-ChildItem.md)

[Get-Content](Get-Content.md)

[ForEach-Object](../Microsoft.PowerShell.Core/ForEach-Object.md)

[New-Item](New-Item.md)
