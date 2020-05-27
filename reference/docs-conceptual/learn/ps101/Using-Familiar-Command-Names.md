---
ms.date: 08/27/2018
keywords: powershell,командлет
title: Использование знакомых имен команд
ms.openlocfilehash: 30b33bc8739975c1a40e51c04a3ee4e426c199e7
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809430"
---
# <a name="using-familiar-command-names"></a>Использование знакомых имен команд

PowerShell поддерживает псевдонимы для вызова команд с помощью альтернативных имен. Благодаря наличию псевдонимов пользователи с опытом работы с другими оболочками могут использовать уже известные им распространенные имена команд для выполнения схожих операций в PowerShell.

Механизм псевдонимов заключается в связывании нового имени с определенной командой. Например, в PowerShell есть внутренняя функция с именем `Clear-Host`, которая очищает командное окно. Вы можете ввести в командной строке псевдоним `cls` или `clear`. PowerShell интерпретирует эти псевдонимы и запускает функцию `Clear-Host`.

Это помогает пользователям изучать PowerShell. Большинство пользователей **cmd.exe** и Unix используют обширный набор команд со знакомыми именами. Их эквиваленты в PowerShell могут возвращать отличающиеся результаты. Но эти результаты достаточно схожи, чтобы пользователи могли работать, не зная имя соответствующей команды PowerShell. Моторная память — еще один источник неудобств при изучении новой командной оболочки. Если вы много лет использовали **cmd.exe**, вы можете по привычке ввести команду `cls`, чтобы очистить экран. Если псевдоним для `Clear-Host` не настроен, вы получите сообщение об ошибке и не будете знать, как очистить экран.

В списке ниже перечислен ряд распространенных команд **cmd.exe** и Unix, которые можно использовать в PowerShell.

|||||
|-|-|-|-|
|cat|dir|подключить|rm|
|компакт-диск|echo (вывод на экран)|перенос|rmdir|
|chdir|erase|popd|sleep|
|clear|h|ps|sort|
|cls|history|pushd|tee|
|copy|kill|pwd|type|
|del|lp|r|запись|
|diff|ls|ren||

Командлет `Get-Alias` показывает исходное имя собственный команды PowerShell, связанной с псевдонимом.

```powershell
PS> Get-Alias cls
```

```Output
CommandType     Name                               Version    Source
-----------     ----                               -------    ------
Alias           cls -> Clear-Host
```

## <a name="interpreting-standard-aliases"></a>Интерпретация стандартных псевдонимов

Описанные выше псевдонимы предназначены для обеспечения совместимости имен, используемых в других командных оболочках.
Большинство встроенных псевдонимов PowerShell созданы для краткости. Более короткие имена проще ввести, но их сложнее читать, если не знать, что они означают.

Псевдонимы PowerShell — это попытка найти компромисс между ясностью и краткостью. PowerShell использует стандартный набор псевдонимов для распространенных существительных и глаголов.

Пример сокращений:

| Существительное или глагол | Сокращение |
|--------------|--------------|
| Получить          | g            |
| Присвойте параметру          | s            |
| Элемент         | i            |
| Location     | l            |
| Get-Help      | cm           |
| Псевдоним        | al           |

Эти псевдонимы легко понять, если вы знаете краткие имена.

| Имя командлета    | Псевдоним |
|----------------|-------|
| `Get-Item`     | gi    |
| `Set-Item`     | si    |
| `Get-Location` | gl    |
| `Set-Location` | sl    |
| `Get-Command`  | gcm   |
| `Get-Alias`    | gal   |

Когда вы изучите псевдонимы PowerShell, вы сразу догадаетесь, что псевдоним **sal** соответствует `Set-Alias`.

## <a name="creating-new-aliases"></a>Создание псевдонимов

Собственные псевдонимы можно создать с помощью командлета `Set-Alias`. Например, указанные ниже инструкции создают описанные выше стандартные псевдонимы командлетов.

```powershell
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

Сама оболочка PowerShell использует похожие команды во время запуска, но эти псевдонимы нельзя изменить.
Если вы попытаетесь выполнить одну из перечисленных выше команд, вы получите ошибку с сообщением о том, что псевдоним изменить невозможно. Пример:

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```