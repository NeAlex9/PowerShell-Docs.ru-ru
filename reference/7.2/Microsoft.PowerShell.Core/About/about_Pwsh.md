---
description: Объясняет, как использовать `pwsh` интерфейс командной строки. Отображает параметры командной строки и описание синтаксиса.
ms.date: 10/05/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pwsh?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Pwsh
ms.openlocfilehash: b31563dd7058d85eb76f34c61d9bff5558a786b0
ms.sourcegitcommit: bf07cffb2a66dec94bf3576e197090f958701f18
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2020
ms.locfileid: "99599625"
---
# <a name="about-pwsh"></a>О pwsh

## <a name="short-description"></a>Краткое описание
Объясняет, как использовать `pwsh` интерфейс командной строки. Отображает параметры командной строки и описание синтаксиса.

## <a name="long-description"></a>Полное описание

## <a name="syntax"></a>Синтаксис

```
pwsh[.exe]
   [[-File] <filePath> [args]]
   [-Command { - | <script-block> [-args <arg-array>]
                 | <string> [<CommandParameters>] } ]
   [-ConfigurationName <string>]
   [-CustomPipeName <string>]
   [-EncodedCommand <Base64EncodedCommand>]
   [-ExecutionPolicy <ExecutionPolicy>]
   [-InputFormat {Text | XML}]
   [-Interactive]
   [-Login]
   [-MTA]
   [-NoExit]
   [-NoLogo]
   [-NonInteractive]
   [-NoProfile]
   [-OutputFormat {Text | XML}]
   [-SettingsFile <SettingsFilePath>]
   [-SSHServerMode]
   [-STA]
   [-Version]
   [-WindowStyle <style>]
   [-WorkingDirectory <directoryPath>]

pwsh[.exe] -h | -Help | -? | /?
```

## <a name="parameters"></a>Параметры

Все параметры не учитывают регистр.

### <a name="-file---f"></a>-File | -f

Если значение `File` равно `-` , текст команды считывается из стандартного ввода.
Запуск `pwsh -File -` без перенаправленного стандартного ввода запускает обычный сеанс. Это то же самое, что не указывает `File` параметр вообще.

Это параметр по умолчанию, если параметры отсутствуют, но в командной строке есть значения. Указанный скрипт выполняется в локальной области ("с источником с точкой"), поэтому функции и переменные, создаваемые сценарием, доступны в текущем сеансе. Введите путь к файлу сценария и любые параметры. Файл должен быть последним параметром в команде, так как все символы, введенные после имени параметра файла, интерпретируется как путь к файлу скрипта, за которым следуют параметры сценария.

Обычно параметры-переключатели сценария включаются или опускаются.
Например, следующая команда использует параметр ALL файла скрипта Get-Script.ps1: `-File .\Get-Script.ps1 -All`

В редких случаях может потребоваться указать **логическое** значение для параметра Switch. Чтобы предоставить **логическое** значение для параметра-переключателя в значении параметра **File** , используйте параметр, обычно за которым следует двоеточие и логическое значение, как показано ниже: `-File .\Get-Script.ps1 -All:$False` .

Передаваемые в скрипт параметры имеют вид строк литералов (после интерпретации текущей оболочкой). Например, если вы используете `cmd.exe` и хотите передать значение переменной среды, используйте `cmd.exe` следующий синтаксис: `pwsh -File .\test.ps1 -TestParam %windir%`

В отличие от этого, выполнение `pwsh -File .\test.ps1 -TestParam $env:windir` в `cmd.exe` дает скрипт, получающий литеральную строку, `$env:windir` так как он не имеет специального значения для текущей `cmd.exe` оболочки. `$env:windir`Стиль ссылки на переменную среды _можно_ использовать внутри параметра **команды** , так как он интерпретируется как код PowerShell.

Аналогично, если вы хотите выполнить ту же команду из _пакетного скрипта_, используйте `%~dp0` вместо `.\` или `$PSScriptRoot` для представления текущего каталога выполнения: `pwsh -File %~dp0test.ps1 -TestParam %windir%` . Если вместо этого используется `.\test.ps1` , PowerShell выдаст ошибку, так как не может найти литеральный путь. `.\test.ps1`

Когда файл скрипта завершается `exit` командой, код завершения процесса задается в виде числового аргумента, используемого с `exit` командой. При нормальном завершении код выхода всегда имеет значение `0` .

Как `-Command` и при возникновении ошибки, завершающей выполнение скрипта, код выхода имеет значение `1` . Однако в отличие от `-Command` , когда выполнение прерывается с помощью <kbd>клавиши CTRL</kbd> - <kbd>C</kbd> , код выхода имеет значение `0` .

### <a name="-command---c"></a>-Command | -c

Выполняет указанные команды (и любые параметры), как если бы они были введены в командной строке PowerShell, а затем завершает работу, если `NoExit` не указан параметр.

Значение **команды** может быть `-` , блоком скрипта или строкой. Если значение **Command** равно `-` , текст команды считывается из стандартного ввода.

Параметр **команды** принимает блок сценария только для выполнения, если он может распознать значение, передаваемое **команде** , в качестве типа **ScriptBlock** . Это возможно _только_ при запуске `pwsh` с другого узла PowerShell. Тип **ScriptBlock** может содержаться в существующей переменной, возвращенной из выражения, или в процессе анализа узлом PowerShell в виде литерального блока скрипта, заключенного в фигурные скобки ( `{}` ), перед передачей в `pwsh` .

```powershell
pwsh -Command {Get-WinEvent -LogName security}
```

В не `cmd.exe` существует такого понятия, как блок сценария (или тип **ScriptBlock** ), поэтому значение, передаваемое **команде** , _всегда_ будет строкой. Вы можете написать блок сценария в строке, но вместо выполнения его поведение будет таким, как если бы вы набирали его в типичном приглашении PowerShell, возвращая содержимое блока сценария обратно.

Строка, передаваемая **команде** , по-прежнему выполняется как код PowerShell, поэтому в первом месте при запуске из не требуется закрывающая фигурная скобка блока script `cmd.exe` . Для выполнения встроенного блока сценария, определенного внутри строки, можно использовать [оператор вызова](about_operators.md#special-operators) `&`.

```
pwsh -Command "& {Get-WinEvent -LogName security}"
```

Если значение **Command** является строкой, **команда** должна быть последним параметром для pwsh, так как все приведенные ниже аргументы будут интерпретироваться как часть выполняемой команды.

При вызове из существующего сеанса PowerShell результаты возвращаются в родительскую оболочку как десериализованные объекты XML, а не в активные объекты. Для других оболочек результаты возвращаются в виде строк.

Если значение **Command** равно `-` , текст команды считывается из стандартного ввода. При использовании параметра **команды** со стандартным входом необходимо перенаправить стандартный ввод. Пример:

```powershell
@'
"in"

"hi" |
  % { "$_ there" }

"out"
'@ | powershell -NoProfile -Command -
```

В этом примере выводятся следующие данные:

```Output
in
hi there
out
```

Код завершения процесса определяется состоянием последней команды (выполненной) в блоке скрипта. Код выхода — `0` когда `$?` имеет значение `$true` или `1` когда `$?` имеет значение `$false` . Если последняя команда является внешней программой или скриптом PowerShell, который явно задает код выхода, отличный от `0` или `1` , то код выхода преобразуется в `1` для кода завершения процесса. Чтобы сохранить конкретный код выхода, добавьте `exit $LASTEXITCODE` в командную строку или блок скрипта.

Аналогичным образом, значение 1 возвращается при ошибке завершения скрипта (прекращение выполнения, завершающейся), например `throw` , или `-ErrorAction Stop` при прерывании выполнения с помощью <kbd>клавиши CTRL</kbd> - <kbd>C</kbd>.

### <a name="-configurationname---config"></a>-ConfigurationName | -config

Указывает конечную точку конфигурации, в которой выполняется PowerShell. Это может быть любая конечная точка, зарегистрированная на локальном компьютере, включая конечные точки удаленного взаимодействия PowerShell по умолчанию или пользовательскую конечную точку с конкретными возможностями роли пользователя.

Например, `pwsh -ConfigurationName AdminRoles`.

### <a name="-custompipename"></a>-Кустомпипенаме

Указывает имя, используемое для дополнительного сервера IPC (именованного канала), используемого для отладки и других межпроцессных соединений. Это обеспечивает предсказуемый механизм подключения к другим экземплярам PowerShell. Обычно используется с параметром **кустомпипенаме** в `Enter-PSHostProcess` .

Этот параметр появился в PowerShell 6,2.

Пример:

```powershell
# PowerShell instance 1
pwsh -CustomPipeName mydebugpipe
# PowerShell instance 2
Enter-PSHostProcess -CustomPipeName mydebugpipe
```

### <a name="-encodedcommand---e---ec"></a>-Енкодедкомманд | -e | -EC

Принимает строковую версию команды в кодировке Base64. Используйте этот параметр, чтобы отправлять команды в PowerShell, требующие сложных вложенных заключения в кавычки. Представление в формате Base64 должно быть строкой в кодировке UTF-16LE.

Пример:

```powershell
$command = 'dir "c:\program files" '
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
pwsh -encodedcommand $encodedCommand
```

### <a name="-executionpolicy---ex---ep"></a>-ExecutionPolicy | -ex | -EP

Задает политику выполнения по умолчанию для текущего сеанса и сохраняет ее в `$env:PSExecutionPolicyPreference` переменной среды. Этот параметр не изменяет постоянно настроенные политики выполнения.

Этот параметр применяется только к компьютерам Windows. `$env:PSExecutionPolicyPreference`Переменная среды не существует на платформах, отличных от Windows.

### <a name="-inputformat---inp---if"></a>-Инпутформат | -INP | — Если

Описывает формат данных, отправляемых в PowerShell. Допустимые значения: "Text" (текстовые строки) или "XML" (сериализованный формат CLIXML).

### <a name="-interactive---i"></a>-Interactive | -i

Предоставление пользователю интерактивного запроса. Обратная для неинтерактивного параметра.

### <a name="-login---l"></a>-Login | -l

В Linux и macOS запускает PowerShell в качестве оболочки входа, используя/bin/sh для выполнения профилей входа, таких как/ЕТК/профиле и ~/.профиле.
В Windows этот параметр не выполняет никаких действий.

> [!IMPORTANT]
> Для запуска PowerShell в качестве оболочки входа этот параметр сначала должен быть первым.
> Передача этого параметра в другую точку будет проигнорирована.

Для настройки в `pwsh` качестве оболочки входа в операционных системах, аналогичных UNIX, выполните следующие действия.

- Убедитесь, что полный абсолютный путь в `pwsh` списке `/etc/shells`
  - Этот путь обычно имеет примерно следующий результат: `/usr/bin/pwsh` в Linux или `/usr/local/bin/pwsh` на macOS
  - При использовании некоторых методов установки эта запись будет добавлена автоматически во время установки.
  - Если отсутствует `pwsh` в `/etc/shells` , используйте редактор для добавления пути к `pwsh` последней строке. Для изменения требуются повышенные привилегии.
- Используйте служебную программу [ЧШ](https://linux.die.net/man/1/chsh) , чтобы настроить оболочку текущего пользователя для `pwsh` :

  ```sh
  chsh -s /usr/bin/pwsh
  ```

> [!WARNING]
> Настройка `pwsh` в качестве оболочки входа в настоящее время не поддерживается в подсистеме Windows для Linux (WSL), и попытка установить `pwsh` ее в качестве оболочки входа в систему может привести к невозможности запуска WSL в интерактивном режиме.

### <a name="-mta"></a>-MTA

Запустите PowerShell с помощью многопоточного подразделения. Этот параметр доступен только в Windows.

### <a name="-noexit---noe"></a>-Exit | -ное

Не завершает работу после выполнения команд запуска.

Например, `pwsh -NoExit -Command Get-Date`.

### <a name="-nologo---nol"></a>-Неэмблема | -Нол

Скрывает баннер авторского права при запуске интерактивных сеансов.

### <a name="-noninteractive---noni"></a>-Неинтерактивный | -Нони

Не предоставляет пользователю интерактивную командную строку. Любые попытки использования интерактивных функций, таких как `Read-Host` или запросы подтверждения, приводят к ошибкам, завершающим выполнение инструкции.

### <a name="-noprofile---nop"></a>-Непрофиль | -NOP

Не загружает профили PowerShell.

### <a name="-outputformat---o---of"></a>-OutputFormat | -o | -of

Определяет формат выходных данных PowerShell. Допустимые значения: "Text" (текстовые строки) или "XML" (сериализованный формат CLIXML).

Например, `pwsh -o XML -c Get-Date`.

При вызове с помощью сеанса PowerShell вы получаете десериализованные объекты как выходные данные, а не обычные строки. При вызове из других оболочек выходными данными являются строковые данные, отформатированные как текст CLIXML.

### <a name="-settingsfile---settings"></a>-SettingsFile | -параметры

Переопределяет файл параметров на уровне системы `powershell.config.json` для сеанса. По умолчанию параметры на уровне системы считываются из в `powershell.config.json` `$PSHOME` каталоге.

Обратите внимание, что эти параметры не используются конечной точкой, заданной `-ConfigurationName` аргументом.

Например, `pwsh -SettingsFile c:\myproject\powershell.config.json`.

### <a name="-sshservermode---sshs"></a>-Сшсервермоде | -сшс

Используется в sshd_config для запуска PowerShell в качестве подсистемы SSH. Он не предназначен для использования в каких-либо других целях.

### <a name="-sta"></a>-STA

Запустите PowerShell с помощью однопотокового подразделения. Это значение по умолчанию. Этот параметр доступен только в Windows.

### <a name="-version---v"></a>-Version | -v

Отображает версию PowerShell. Дополнительные параметры игнорируются.

### <a name="-windowstyle---w"></a>-WindowStyle | -w

Задает стиль окна для сеанса. Допустимые значения: Normal, Minimized, Maximized и Hidden.

### <a name="-workingdirectory---wd"></a>-WorkingDirectory | — WD

Задает начальный рабочий каталог, выполняя при запуске. Поддерживается любой допустимый путь к файлу PowerShell.

Чтобы запустить PowerShell в домашнем каталоге, используйте: `pwsh -WorkingDirectory ~`

### <a name="-help---"></a>-Help, -?, /?

Отображает справку для `pwsh` . При вводе команды pwsh в PowerShell добавляйте параметры команды с дефисом ( `-` ), а не косой чертой ( `/` ).
