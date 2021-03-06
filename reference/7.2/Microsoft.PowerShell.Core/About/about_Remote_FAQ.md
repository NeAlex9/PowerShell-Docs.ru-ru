---
description: Содержит вопросы и ответы о выполнении удаленных команд в PowerShell.
Locale: en-US
ms.date: 07/23/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Remote_FAQ
ms.openlocfilehash: da3516697c58e3273538ed2ed93a7a54fcd9bb49
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "99599373"
---
# <a name="about-remote-faq"></a>about_Remote_FAQ

## <a name="short-description"></a>Краткое описание
Содержит вопросы и ответы о выполнении удаленных команд в PowerShell.

## <a name="long-description"></a>Подробное описание

При удаленной работе вы вводите команды в PowerShell на одном компьютере (называемом "локальный компьютер"), но команды запускаются на другом компьютере (называемом "удаленным компьютером"). Работа по удаленному интерфейсу должна быть настолько, насколько это возможно, непосредственно на удаленном компьютере.

Примечание. чтобы использовать удаленное взаимодействие PowerShell, необходимо настроить удаленный компьютер для удаленного взаимодействия. Дополнительные сведения см. в разделе [about_Remote_Requirements](about_Remote_Requirements.md).

### <a name="must-both-computers-have-powershell-installed"></a>Необходимо ли установить PowerShell на обоих компьютерах?

Да. Для удаленной работы на локальном и удаленном компьютерах должны быть установлены PowerShell, платформа Microsoft .NET и веб-службы для управления (WS-Management). Все файлы и другие ресурсы, необходимые для выполнения определенной команды, должны находиться на удаленном компьютере.

Компьютеры, на которых выполняется Windows PowerShell 3,0 и компьютеры с Windows PowerShell 2,0, могут подключаться друг к другу удаленно и выполнять удаленные команды.
Однако некоторые функции, например возможность отключения от сеанса и повторного подключения к нему, работают только в том случае, если оба компьютера работают под управлением Windows PowerShell 3,0.

Необходимо иметь разрешение на подключение к удаленному компьютеру, разрешение на запуск PowerShell и разрешение на доступ к хранилищам данных (например, файлам и папкам) и реестру на удаленном компьютере.

Дополнительные сведения см. в разделе [about_Remote_Requirements](about_Remote_Requirements.md).

### <a name="how-does-remoting-work"></a>Как работает удаленное взаимодействие?

При отправке удаленной команды команда передается по сети модулю PowerShell на удаленном компьютере и выполняется в клиенте PowerShell на удаленном компьютере. Результаты команды отправляются обратно на локальный компьютер и отображаются в сеансе PowerShell на локальном компьютере.

Для передачи команд и получения выходных данных PowerShell использует протокол WS-Management. Дополнительные сведения о протоколе WS-Management см. в разделе [протокол WS-Management](/windows/win32/winrm/ws-management-protocol) документации по Windows.

Начиная с Windows PowerShell 3,0, удаленные сеансы хранятся на удаленном компьютере. Это позволяет отключиться от сеанса и повторно подключиться из другого сеанса или другого компьютера без прерывания команд или потери состояния.

### <a name="is-powershell-remoting-secure"></a>Безопасна ли служба удаленного взаимодействия PowerShell?

При подключении к удаленному компьютеру система использует учетные данные пользователя и пароля на локальном компьютере или учетные данные, предоставленные в команде для входа на удаленный компьютер. Учетные данные и остальная часть передачи шифруются.

Чтобы добавить дополнительную защиту, можно настроить удаленный компьютер на использование SSL (SSL) вместо HTTP для прослушивания запросов служба удаленного управления Windows (WinRM). Затем при установлении соединения пользователи  могут использовать параметр UseSSL `Invoke-Command` `New-PSSession` `Enter-PSSession` командлетов, и. Этот параметр использует более защищенный канал HTTPS вместо HTTP.

### <a name="do-all-remote-commands-require-powershell-remoting"></a>Требуется ли удаленное взаимодействие PowerShell для всех удаленных команд?

Нет. Несколько командлетов имеют параметр **ComputerName** , позволяющий получать объекты с удаленного компьютера.

Эти командлеты не используют удаленное взаимодействие PowerShell. Поэтому их можно использовать на любом компьютере, на котором работает PowerShell, даже если компьютер не настроен для удаленного взаимодействия PowerShell или компьютер не соответствует требованиям удаленного взаимодействия PowerShell.

К этим командлетам относятся следующие:

- `Get-Process`
- `Get-Service`
- `Get-WinEvent`
- `Get-EventLog`
- `Test-Connection`

Чтобы найти все командлеты с параметром **ComputerName** , введите:

```powershell
Get-Help * -Parameter ComputerName
# or
Get-Command -ParameterName ComputerName
```

Чтобы определить, требуется ли для параметра **ComputerName** конкретного командлета удаленное взаимодействие PowerShell, см. Описание параметра. Чтобы отобразить описание параметра, введите:

```powershell
Get-Help <cmdlet-name> -Parameter ComputerName
```

Пример:

```powershell
Get-Help Get-Process -Parameter ComputerName
```

Для всех остальных команд используйте `Invoke-Command` командлет.

### <a name="how-do-i-run-a-command-on-a-remote-computer"></a>Разделы справки выполнить команду на удаленном компьютере?

Чтобы выполнить команду на удаленном компьютере, используйте `Invoke-Command` командлет.

Заключите команду в фигурные скобки ( `{}` ), чтобы сделать ее блоком сценария. Используйте параметр **ScriptBlock** аргумента `Invoke-Command` для указания команды.

Параметр **ComputerName** параметра можно использовать `Invoke-Command` для указания удаленного компьютера. Или можно создать постоянное подключение к удаленному компьютеру (сеанс), а затем использовать параметр **Session** из `Invoke-Command` для выполнения команды в сеансе.

Например, следующие команды выполняют `Get-Process` команду удаленно.

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-Process}

#  - OR -

Invoke-Command -Session $s -ScriptBlock {Get-Process}
```

Чтобы прервать удаленную команду, введите <kbd>CTRL</kbd> + <kbd>C</kbd>. Запрос на прерывание передается на удаленный компьютер, где он завершает удаленную команду.

Дополнительные сведения об удаленных командах см. в разделе about_Remote и разделы справки по командлетам, поддерживающим удаленное взаимодействие.

### <a name="can-i-just-telnet-into-a-remote-computer"></a>Могу ли я только Telnet на удаленном компьютере?

`Enter-PSSession`С помощью командлета можно запустить интерактивный сеанс с удаленным компьютером.

В командной строке PowerShell введите следующую команду:

```powershell
Enter-PSSession <ComputerName>
```

Командная строка изменится, чтобы отображалось подключение к удаленному компьютеру.

```
<ComputerName>\C:>
```

Теперь команды, которые вы вводите, выполняются на удаленном компьютере так же, как и при их вводе непосредственно на удаленном компьютере.

Чтобы завершить интерактивный сеанс, введите:

```powershell
Exit-PSSession
```

Интерактивный сеанс — это постоянный сеанс, использующий протокол WS-Management. Это не то же самое, что и Telnet, но обеспечивает аналогичную работу.

Для получения дополнительной информации см. `Enter-PSSession`.

### <a name="can-i-create-a-persistent-connection"></a>Можно ли создать постоянное подключение?

Да. Для выполнения удаленных команд можно указать имя удаленного компьютера, имя NetBIOS или его IP-адрес. Также можно выполнить удаленные команды, указав сеанс PowerShell (PSSession), подключенный к удаленному компьютеру.

При использовании параметра **ComputerName** в `Invoke-Command` или `Enter-PSSession` PowerShell устанавливает временное подключение. PowerShell использует соединение для выполнения только текущей команды, а затем закрывает соединение. Это очень эффективный метод выполнения одной команды или нескольких несвязанных команд, даже на многих удаленных компьютерах.

При использовании `New-PSSession` командлета для создания сеанса PSSession PowerShell устанавливает постоянное подключение к сеансу PSSession. Затем можно выполнить несколько команд в сеансе PSSession, включая команды, которые совместно используют данные.

Как правило, сеанс PSSession создается для выполнения ряда связанных команд, которые совместно используют данные. В противном случае для большинства команд достаточно временное соединение, созданное параметром **ComputerName** .

Дополнительные сведения о сеансах см. в разделе about_PSSessions.

### <a name="can-i-run-commands-on-more-than-one-computer-at-a-time"></a>Можно ли выполнять команды более чем на одном компьютере за раз?

Да. Параметр **ComputerName** `Invoke-Command` командлета принимает несколько имен компьютеров, а параметр **Session** принимает несколько PSSession.

При выполнении `Invoke-Command` команды PowerShell выполняет команды на всех указанных компьютерах или во всех указанных PSSession.

PowerShell может управлять сотнями одновременных удаленных подключений. Однако количество удаленных команд, которые можно отправить, может быть ограничено ресурсами компьютера и его емкостью для установки и обслуживания нескольких сетевых подключений.

Дополнительные сведения см. в примере в `Invoke-Command` разделе справки.

### <a name="where-are-my-profiles"></a>Где находятся мои профили?

Профили PowerShell не запускаются автоматически в удаленных сеансах, поэтому команды, добавляемые в профиль, отсутствуют в сеансе. Кроме того, `$profile` Автоматическая переменная не заполняется в удаленных сеансах.

Чтобы запустить профиль в сеансе, используйте `Invoke-Command` командлет.

Например, следующая команда запускает профиль CurrentUserCurrentHost с локального компьютера в сеансе `$s` .

```
Invoke-Command -Session $s -FilePath $profile
```

Следующая команда запускает профиль CurrentUserCurrentHost с удаленного компьютера в сеансе в `$s` . Так как `$profile` переменная не заполнена, команда использует явный путь к профилю.

```powershell
Invoke-Command -Session $s {
  . "$home\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1"
}
```

После выполнения этой команды команды, которые профиль добавляет в сеанс, будут доступны в `$s` .

Сценарий запуска можно также использовать в конфигурации сеанса для запуска профиля в каждом удаленном сеансе, использующем конфигурацию сеанса.

Дополнительные сведения о профилях PowerShell см. в разделе about_Profiles.
Дополнительные сведения о конфигурациях сеансов см. в разделе `Register-PSSessionConfiguration` .

### <a name="how-does-throttling-work-on-remote-commands"></a>Как работает регулирование для удаленных команд?

Чтобы упростить управление ресурсами на локальном компьютере, в PowerShell имеется функция регулирования для отдельных команд, которая позволяет ограничить количество одновременных удаленных подключений, установленных для каждой команды.

Значение по умолчанию — 32 одновременных подключений, но можно использовать параметр **ThrottleLimit** командлетов, чтобы установить настраиваемое ограничение регулирования для определенных команд.

При использовании функции регулирования Помните, что она применяется к каждой команде, а не ко всему сеансу или к компьютеру. При одновременном выполнении команд в нескольких сеансах или PSSession число одновременных подключений равно сумме одновременных подключений во всех сеансах.

Чтобы найти командлеты с параметром **ThrottleLimit** , введите:

```
Get-Help * -Parameter ThrottleLimit
-or-
Get-Command -ParameterName ThrottleLimit
```

### <a name="is-the-output-of-remote-commands-different-from-local-output"></a>Отличаются ли выходные данные удаленных команд от локального вывода?

При использовании PowerShell в локальной среде вы отправляете и получаете "динамические" платформа .NET Framework объекты; "динамические" объекты — это объекты, связанные с фактическими программами или системными компонентами. При вызове методов или изменении свойств активных объектов изменения влияют на фактическую программу или компонент. А при изменении свойств программы или компонента свойства объекта, которые их представляют, также изменяются.

Однако поскольку большинство активных объектов не могут передаваться по сети, PowerShell «сериализует» большинство объектов, отправленных в удаленных командах, то есть преобразует каждый объект в ряд элементов данных XML (язык ограничений в XML [CLiXML]) для передачи.

Когда PowerShell получает сериализованный объект, он преобразует XML в тип десериализованного объекта. Десериализованный объект — это точная запись свойств программы или компонента в предыдущий раз, но она больше не является "динамической", то есть больше не связана напрямую с компонентом. Методы удаляются, так как они больше не действуют.

Как правило, десериализуемые объекты можно использовать так же, как и активные объекты, но следует иметь в виду их ограничения. Кроме того, объекты, возвращаемые `Invoke-Command` командлетом, имеют дополнительные свойства, помогающие определить происхождение команды.

Некоторые типы объектов, например объекты DirectoryInfo и GUID, преобразуются обратно в динамические объекты при их получении. Для этих объектов не требуется специальная обработка или форматирование.

Дополнительные сведения об интерпретации и форматировании удаленных выходных данных см. в разделе [about_Remote_Output](about_Remote_Output.md).

### <a name="can-i-run-background-jobs-remotely"></a>Можно ли выполнять фоновые задания удаленно?

Да. Фоновое задание PowerShell — это команда PowerShell, которая выполняется асинхронно без взаимодействия с сеансом. При запуске фонового задания командная строка возвращается немедленно, и вы можете продолжать работу в сеансе, пока задание выполняется, даже если оно выполняется в течение продолжительного периода времени.

Фоновое задание можно запустить даже во время выполнения других команд, так как фоновые задания всегда выполняются асинхронно во временном сеансе.

Фоновые задания можно выполнять на локальном или удаленном компьютере. По умолчанию фоновое задание выполняется на локальном компьютере. Однако можно использовать параметр **AsJob** `Invoke-Command` командлета для выполнения любой удаленной команды в качестве фонового задания. И можно использовать `Invoke-Command` для `Start-Job` удаленного выполнения команды.

Дополнительные сведения о фоновых заданиях в PowerShell см. в разделе [about_Jobs (about_Jobs. md)] и [about_Remote_Jobs (about_Remote_Jobs. md)].

### <a name="can-i-run-windows-programs-on-a-remote-computer"></a>Можно ли запускать программы Windows на удаленном компьютере?

Для запуска программ на основе Windows на удаленных компьютерах можно использовать удаленные команды PowerShell. Например, можно запустить `Shutdown.exe` или `Ipconfig.exe` на удаленном компьютере.

Однако нельзя использовать команды PowerShell для открытия пользовательского интерфейса для любой программы на удаленном компьютере.

При запуске программы Windows на удаленном компьютере команда не завершается, и Командная строка PowerShell не возвращается, пока программа не будет завершена или пока не будет нажата клавиша <kbd>CTRL</kbd> + <kbd>C</kbd> для прерывания команды. Например, если запустить `Ipconfig.exe` программу на удаленном компьютере, Командная строка не вернется, пока не `Ipconfig.exe` завершится.

При использовании удаленных команд для запуска программы с пользовательским интерфейсом запускается процесс, но пользовательский интерфейс не отображается. Команда PowerShell не завершена, и Командная строка не будет возвращаться до тех пор, пока не будет остановлен процесс программы или пока не нажата клавиша <kbd>CTRL</kbd> + <kbd>C</kbd>, которая прерывает выполнение команды и останавливает процесс.

Например, если для запуска `Notepad` на удаленном компьютере используется команда PowerShell, процесс «Блокнот» запускается на удаленном компьютере, но пользовательский интерфейс блокнота не отображается. Чтобы прервать выполнение команды и восстановить командную строку, нажмите клавиши <kbd>CTRL</kbd> + <kbd>C</kbd>.

### <a name="can-i-limit-the-commands-that-users-can-run-remotely-on-my-computer"></a>Можно ли ограничить команды, которые пользователи могут запускать удаленно на моем компьютере?

Да. Каждый удаленный сеанс должен использовать одну из конфигураций сеанса на удаленном компьютере. Вы можете управлять конфигурациями сеансов на компьютере (и разрешениями для этих конфигураций сеанса), чтобы определить, кто может выполнять команды удаленно на компьютере и какие команды они могут выполняться.

Конфигурация сеанса настраивает среду для сеанса. Конфигурацию можно определить с помощью сборки, реализующей новый класс конфигурации, или с помощью скрипта, выполняемого в сеансе. Конфигурация может определять команды, доступные в сеансе.
Кроме того, конфигурация может включать параметры, защищающие компьютер, такие как параметры, ограничивающие объем данных, которые сеанс может получить удаленно, в одном объекте или команде. Можно также указать дескриптор безопасности, который определяет разрешения, необходимые для использования конфигурации.

`Enable-PSRemoting`Командлет создает конфигурации сеансов по умолчанию на компьютере: Microsoft. PowerShell, Microsoft. PowerShell. Workflow и Microsoft. PowerShell32 (только 64-разрядные операционные системы). `Enable-PSRemoting` Задает дескриптор безопасности для конфигурации, чтобы разрешить использовать их только членам группы "Администраторы" на компьютере.

Командлеты конфигурации сеанса можно использовать для изменения конфигураций сеансов по умолчанию, создания новых конфигураций сеансов и изменения дескрипторов безопасности всех конфигураций сеансов.

Начиная с Windows PowerShell 3,0, `New-PSSessionConfigurationFile` командлет позволяет создавать пользовательские конфигурации сеансов с помощью текстового файла. Файл содержит параметры для настройки языкового режима и для указания командлетов и модулей, доступных в сеансах, использующих конфигурацию сеанса.

Когда пользователи используют `Invoke-Command` `New-PSSession` командлеты,, или `Enter-PSSession` , они могут использовать параметр **configurationName** для указания конфигурации сеанса, используемой для сеанса. Кроме того, они могут изменить конфигурацию по умолчанию, которую используют сеансы, изменив значение `$PSSessionConfigurationName` переменной предпочтений в сеансе.

Дополнительные сведения о конфигурациях сеансов см. в справке по командлетам конфигурации сеанса. Чтобы найти командлеты конфигурации сеанса, введите:

```powershell
Get-Command *PSSessionConfiguration
```

### <a name="what-are-fan-in-and-fan-out-configurations"></a>Что такое конфигурации вентиляторов и наружных вентиляторов?

Наиболее распространенным сценарием удаленного взаимодействия PowerShell, включающим несколько компьютеров, является конфигурация "один ко многим", в которой один локальный компьютер (компьютер администратора) выполняет команды PowerShell на многочисленных удаленных компьютерах. Этот сценарий называется "выходом из".

Однако на некоторых предприятиях конфигурация имеет значение «многие к одному», где многие клиентские компьютеры подключаются к одному удаленному компьютеру, работающему под управлением PowerShell, например файловый сервер или киоск. Это называется конфигурацией с вентилятором.

Удаленное взаимодействие PowerShell поддерживает конфигурации как развертывания, так и вентилятора.

Для конфигурации с выходом из развертывания PowerShell использует протокол веб-служб для управления (WS-Management) и службу WinRM, поддерживающую реализацию WS-Management Майкрософт. При подключении локального компьютера к удаленному компьютеру WS-Management устанавливает подключение и использует подключаемый модуль для PowerShell, чтобы запустить хост-процесс PowerShell (Wsmprovhost.exe) на удаленном компьютере. Пользователь может указать альтернативный порт, конфигурацию дополнительного сеанса и другие функции для настройки удаленного подключения.

Для поддержки конфигурации "с вентиляторами" в PowerShell используются службы IIS для размещения WS-Management, загрузки подключаемого модуля PowerShell и запуска PowerShell. В этом сценарии вместо того, чтобы запускать каждый сеанс PowerShell в отдельном процессе, все сеансы PowerShell выполняются в одном и том же хост-процессе.

Размещение и удаленное управление в IIS не поддерживается в Windows XP и Windows Server 2003.

В конфигурации с вентилятором пользователь может указать универсальный код ресурса (URI) подключения и конечную точку HTTP, включая транспорт, имя компьютера, порт и имя приложения.
Службы IIS пересылают в приложение все запросы с указанным именем приложения. Значение по умолчанию — WS-Management, в котором может размещаться PowerShell.

Можно также указать механизм проверки подлинности и запретить или разрешить перенаправление из конечных точек HTTP и HTTPS.

### <a name="can-i-test-remoting-on-a-single-computer-not-in-a-domain"></a>Можно ли протестировать удаленное взаимодействие на одном компьютере, а не в домене?

Да. Удаленное взаимодействие PowerShell доступно даже в том случае, если локальный компьютер не входит в домен. Функции удаленного взаимодействия можно использовать для подключения к сеансам и создания сеансов на одном компьютере. Функции работают так же, как и при подключении к удаленному компьютеру.

Для выполнения удаленных команд на компьютере в Рабочей группе Измените следующие параметры Windows на компьютере.

Внимание! эти параметры влияют на всех пользователей системы и могут сделать систему более уязвимой для атак злоумышленников. Будьте внимательны при внесении этих изменений.

- Windows Vista, Windows 7, Windows 8:

  Создайте следующую запись реестра и присвойте ей значение 1: LocalAccountTokenFilterPolicy в ` HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`

  Для добавления этой записи можно использовать следующую команду PowerShell:

    ```powershell
    $parameters = @{
      Path='HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System'
      Name='LocalAccountTokenFilterPolicy'
      propertyType='DWord'
      Value=1
    }
    New-ItemProperty @parameters
    ```

- Windows Server 2003, Windows Server 2008, Windows Server 2012, Windows Server 2012 R2:

  Изменения не требуются, так как параметр по умолчанию политики "сетевой доступ: модель общего доступа и безопасность для локальных учетных записей" имеет значение "Классическая". Проверьте значение параметра, если оно изменилось.

### <a name="can-i-run-remote-commands-on-a-computer-in-another-domain"></a>Можно ли выполнять удаленные команды на компьютере в другом домене?

Да. Как правило, команды выполняются без ошибок, хотя может потребоваться использовать параметр **Credential** `Invoke-Command` `New-PSSession` командлета, или, `Enter-PSSession` чтобы предоставить учетные данные члена группы администраторов на удаленном компьютере. Это иногда требуется, даже если текущий пользователь является членом группы "Администраторы" на локальном и удаленном компьютерах.

Однако если удаленный компьютер не входит в домен, которому доверяет локальный компьютер, удаленный компьютер не сможет проверить подлинность учетных данных пользователя.

Чтобы включить проверку подлинности, используйте следующую команду, чтобы добавить удаленный компьютер в список доверенных узлов для локального компьютера в WinRM. Введите команду в командной строке PowerShell.

```powershell
Set-Item WSMan:\localhost\Client\TrustedHosts -Value <Remote-computer-name>
```

Например, чтобы добавить компьютер Server01 в список доверенных узлов на локальном компьютере, введите следующую команду в командной строке PowerShell:

```powershell
Set-Item WSMan:\localhost\Client\TrustedHosts -Value Server01
```

### <a name="does-powershell-support-remoting-over-ssh"></a>Поддерживает ли PowerShell удаленное взаимодействие через SSH?

Да. Дополнительные сведения см. в статье [удаленное взаимодействие PowerShell через SSH](/powershell/scripting/learn/remoting/ssh-remoting-in-powershell-core).

## <a name="see-also"></a>См. также

[about_Remote](about_Remote.md)

[about_Profiles](about_Profiles.md)

[about_PSSessions](about_PSSessions.md)

[about_Remote_Jobs](about_Remote_Jobs.md)

[about_Remote_Variables](about_Remote_Variables.md)

[Invoke-Command](xref:Microsoft.PowerShell.Core.Invoke-Command)

[New-PSSession](xref:Microsoft.PowerShell.Core.New-PSSession)
