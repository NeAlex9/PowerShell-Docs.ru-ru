---
ms.date: 08/21/2020
keywords: powershell,командлет
title: Выполнение удаленных команд
description: Описываются способы выполнения команд в удаленных системах с помощью PowerShell.
ms.openlocfilehash: cff18a4f51c3ed8e3ed2c1f35862a88911e7ceb5
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "94391414"
---
# <a name="running-remote-commands"></a>Выполнение удаленных команд

Одна команда Windows PowerShell позволяет запускать команды на одном или сотнях компьютеров. Windows PowerShell поддерживает удаленное вычисление с помощью разных технологий, включая WMI, RPC и WS-Management.

PowerShell Core поддерживает инструментарий WMI, WS-Management и удаленное взаимодействие через SSH. В PowerShell 6 RPC больше не поддерживается. В PowerShell 7 и более поздних версиях RPC поддерживается только в Windows.

Дополнительные сведения об удаленном взаимодействии в PowerShell Core см. в следующих статьях:

- [Удаленное взаимодействие через SSH в PowerShell Core][ssh-remoting]
- [Удаленное взаимодействие через WSMan в PowerShell Core][wsman-remoting]

## <a name="windows-powershell-remoting-without-configuration"></a>Удаленное взаимодействие с Windows PowerShell без настройки

Многие командлеты Windows PowerShell имеют параметр ComputerName, который позволяет собирать данные и изменять параметры одного или нескольких удаленных компьютеров. Эти командлеты используют разные протоколы связи и работают во всех операционных системах Windows без специальной настройки.

В эти командлеты входят следующие:

- [Restart-Computer](/powershell/module/microsoft.powershell.management/restart-computer)
- [Test-Connection](/powershell/module/microsoft.powershell.management/test-connection)
- [Clear-EventLog](/powershell/module/microsoft.powershell.management/clear-eventlog)
- [Get-EventLog](/powershell/module/microsoft.powershell.management/get-eventlog)
- [Get-HotFix](/powershell/module/microsoft.powershell.management/get-hotfix)
- [Get-Process](/powershell/module/microsoft.powershell.management/get-process)
- [Get-Service](/powershell/module/microsoft.powershell.management/get-service)
- [Set-Service](/powershell/module/microsoft.powershell.management/set-service)
- [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [Get-WmiObject](/powershell/module/microsoft.powershell.management/get-wmiobject)

Обычно командлеты, которые поддерживают удаленное взаимодействие без специальной настройки, имеют параметр ComputerName, но не имеют параметра Session. Чтобы найти эти командлеты в сеансе, введите:

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>Служба удаленного взаимодействия Windows PowerShell

Благодаря использованию протокола WS-Management служба удаленного взаимодействия Windows PowerShell позволяет запустить любую команду Windows PowerShell на одном или нескольких удаленных компьютерах. Вы можете устанавливать постоянные подключения, запускать интерактивные сеансы и выполнять скрипты на удаленных компьютерах.

Чтобы использовать службу удаленного взаимодействия Windows PowerShell, удаленный компьютер должен быть настроен для удаленного управления.
Дополнительные сведения, в том числе инструкции, см. в разделе [about_Remote_Requirements](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).

После настройки службы удаленного взаимодействия Windows PowerShell вы получите доступ ко многим стратегиям удаленного взаимодействия.
В этой статье перечислены только некоторые из них. См. дополнительные сведения об [удаленном взаимодействии](/powershell/module/microsoft.powershell.core/about/about_remote).

### <a name="start-an-interactive-session"></a>Запуск интерактивного сеанса

Чтобы запустить интерактивный сеанс с одним удаленным компьютером, используйте командлет [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession). Например, чтобы запустить интерактивный сеанс с удаленным компьютером Server01, введите:

```powershell
Enter-PSSession Server01
```

В командной строке отобразится имя удаленного компьютера. Все команды, введенные в командной строке, запускаются на удаленном компьютере, а результаты отображаются на локальном компьютере.

Чтобы завершить интерактивный сеанс, введите:

```powershell
Exit-PSSession
```

См. дополнительные сведения о командлетах Enter-PSSession и Exit-PSSession:

- [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession)
- [Exit-PSSession;](/powershell/module/microsoft.powershell.core/exit-pssession)

### <a name="run-a-remote-command"></a>Выполнение удаленной команды

Чтобы выполнить команду на одном или нескольких компьютерах, используйте командлет [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command). Например, чтобы выполнить команду [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) на удаленных компьютерах Server01 и Server02, введите:

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

Выходные данные будут возвращены на ваш компьютер.

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

### <a name="run-a-script"></a>Запуск сценария

Чтобы запустить скрипт на одном или нескольких удаленных компьютерах, используйте параметр FilePath командлета `Invoke-Command`. Сценарий должен быть включен или доступен для локального компьютера. Результаты будут возвращены на локальный компьютер.

Например, следующая команда выполняет скрипт DiskCollect.ps1 на удаленных компьютерах Server01 и Server02.

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

### <a name="establish-a-persistent-connection"></a>Установка постоянного подключения

Используйте командлет `New-PSSession` для создания постоянного сеанса на удаленном компьютере. В следующем примере создаются удаленные сеансы на удаленных компьютерах Server01 и Server02. Объекты сеанса хранятся в переменной `$s`.

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

После установки сеансов в них можно выполнить любую команду. Так как сеансы являются постоянными, вы можете собирать данные из одной команды и использовать их в другой.

Например, следующая команда выполняет команду Get-Hotfix в сеансах в переменной $s и сохраняет результаты в переменной $h. Переменная $h создается в каждом сеансе в переменной $s, но она не существует в локальном сеансе.

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

Теперь вы можете использовать данные в переменной `$h` с другими командами в том же сеансе. Результаты отобразятся на локальном компьютере. Пример:

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Расширенная служба удаленного взаимодействия

Это и есть служба удаленного взаимодействия Windows PowerShell. Используя командлеты, установленные с Windows PowerShell, можно установить и настроить удаленные сеансы с локальных и удаленных компьютеров, создать настраиваемые и ограниченные сеансы, разрешить пользователям импортировать команды из удаленного сеанса, которые могут неявно выполняться в удаленном сеансе, настроить безопасность удаленного сеанса и многое другое.

Windows PowerShell включает поставщик WSMan. Поставщик создает диск `WSMAN:`, который позволяет перемещаться по иерархии параметров конфигурации на локальном и удаленном компьютерах.

См. дополнительные сведения о [поставщике WSMan](/powershell/module/microsoft.wsman.management/about/about_wsman_provider) и [командлетах WS-Management](/powershell/module/microsoft.wsman.management/about/about_ws-management_cmdlets) или введите команду `Get-Help wsman` в консоли Windows PowerShell.

Дополнительные сведения можно найти в разделе

- [Часто задаваемые вопросы об удаленном взаимодействии](/powershell/module/microsoft.powershell.core/about/about_remote_faq)
- [Register-PSSessionConfiguration](xref:Microsoft.PowerShell.Core.Register-PSSessionConfiguration)
- [Import-PSSession](xref:Microsoft.PowerShell.Utility.Import-PSSession)

Справку по ошибкам службы удаленного взаимодействия см. в разделе [about_Remote_Troubleshooting](/powershell/module/microsoft.powershell.core/about/about_Remote_Troubleshooting).

## <a name="see-also"></a>См. также:

- [about_Remote](/powershell/module/microsoft.powershell.core/about/about_remote_faq)
- [about_Remote_FAQ](/powershell/module/microsoft.powershell.core/about/about_remote_faq)
- [about_Remote_Requirements](/powershell/module/microsoft.powershell.core/about/about_remote_requirements)
- [about_Remote_Troubleshooting](/powershell/module/microsoft.powershell.core/about/about_Remote_Troubleshooting)
- [about_PSSessions](/powershell/module/microsoft.powershell.core/about/about_PSSessions)
- [about_WS-Management_Cmdlets](/powershell/module/microsoft.wsman.management/about/about_ws-management_cmdlets)
- [Invoke-Command](xref:Microsoft.PowerShell.Core.Invoke-Command)
- [Import-PSSession](xref:Microsoft.PowerShell.Utility.Import-PSSession)
- [New-PSSession](xref:Microsoft.PowerShell.Core.New-PSSession)
- [Register-PSSessionConfiguration](xref:Microsoft.PowerShell.Core.Register-PSSessionConfiguration)
- [Поставщик WSMan](/powershell/module/microsoft.wsman.management/about/about_wsman_provider)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md
