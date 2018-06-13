---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Получение сведений о командах
ms.assetid: 56f8e5b4-d97c-4e59-abbe-bf13e464eb0d
ms.openlocfilehash: c51579fe2cdf4f2a0d3248d1aaf3f1f9cac83868
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34482732"
---
# <a name="getting-information-about-commands"></a>Получение сведений о командах
Командлет `Get-Command` Windows PowerShell возвращает все команды, доступные в текущем сеансе. При вводе `Get-Command` в командной строке PowerShell появятся выходные данные, аналогичные следующим:

```
PS> Get-Command
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
Cmdlet          Add-Member                      Add-Member [-MemberType] <PS...
...
```

Эти выходные данные выглядят так же, как и выходные данные справки Cmd.exe: сводная таблица внутренних команд. Во фрагменте выходных данных команды **Get-Command**, показанном выше, все команды имеют CommandType командлета. Командлет является встроенным типом команды Windows PowerShell — типом, который примерно соответствует командам **dir** и **cd** Cmd.exe и встроенным командам в оболочках UNIX, например BASH.

В выходных данных команды `Get-Command` все определения заканчиваются многоточием (...), указывая, что PowerShell не может отображать все содержимое в доступном пространстве. При отображении выходных данных через Windows PowerShell служба форматирует их как текст, а затем упорядочивает таким образом, чтобы данные полностью помещались в окне. Об этом речь пойдет далее в разделе о модулях форматирования.

Командлет `Get-Command` содержит параметр **Syntax**, который возвращает синтаксис каждого командлета. Чтобы получить синтаксис командлета Get-Help, используйте следующую команду:

```
Get-Command Get-Help -Syntax

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Full] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Detailed] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Examples] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]

Get-Help [[-Name] <String>] [-Path <String>] [-Category <String[]>] [-Component <String[]>] [-Functionality <String[]>]
 [-Role <String[]>] [-Parameter <String>] [-Online] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>]
```

### <a name="displaying-available-command-types"></a>Отображение доступных типов команд
Команда **Get-Command** не перечисляет все команды, доступные в Windows PowerShell. Вместо этого команда **Get-Command** перечисляет только командлеты в текущем сеансе. Windows PowerShell фактически поддерживает несколько других типов команд. Псевдонимы, функции и скрипты также являются командами Windows PowerShell, хотя они не описываются подробно в руководстве пользователя Windows PowerShell. Внешние файлы, исполняемые или содержащие обработчик зарегистрированных типов файлов, также классифицируются как команды.

Чтобы получить все команды в сеансе, введите следующую команду:

```powershell
Get-Command *
```

Так как этот список включает внешние файлы в пути поиска, они могут содержать тысячи элементов. Полезнее рассмотреть сокращенный набор команд.

Чтобы получить собственные команды других типов, используйте параметр **CommandType** командлета `Get-Command`.

> [!NOTE]
> Звездочка (\*) используется для сопоставления подстановочных знаков в аргументах командной строки Windows PowerShell. Знак "\*" означает "сопоставление одного или нескольких символов". Чтобы найти все команды, которые начинаются с буквы "a", введите `Get-Command a*`. В отличие от сопоставления подстановочных знаков в Cmd.exe, подстановочный знак Windows PowerShell будет также сопоставлять точку.

Чтобы получить псевдонимы команд, которые являются назначенными псевдонимами команд, введите:

```powershell
Get-Command -CommandType Alias
```

Чтобы получить функции текущего сеанса, введите:

```powershell
Get-Command -CommandType Function
```

Чтобы отобразить скрипты в пути поиска Windows PowerShell, введите:

```powershell
Get-Command -CommandType Script
```
