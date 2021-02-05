---
ms.date: 07/10/2019
keywords: jea,powershell,безопасность
title: Аудит и отчеты для JEA
description: Это поможет вам убедиться, что доступ к конечной точке JEA получают уполномоченные для этого люди и что назначенные им роли по-прежнему являются допустимыми.
ms.openlocfilehash: 2140d6b756ae38d82e4943c373e8a75beea30e28
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92500017"
---
# <a name="auditing-and-reporting-on-jea"></a>Аудит и отчеты для JEA

После развертывания JEA требуется регулярно проводить аудит конфигурации JEA. Это поможет вам убедиться, что доступ к конечной точке JEA получают уполномоченные для этого люди и что назначенные им роли по-прежнему являются допустимыми.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Поиск зарегистрированных сеансов JEA на компьютере

Чтобы узнать, какие сеансы JEA зарегистрированы на компьютере, используйте командлет [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration).

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }
```

```Output
Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed,
                CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

Действующие права для конечной точки перечислены в свойстве **Permission**. Эти пользователи имеют право на подключение к конечной точке JEA. Доступные им роли и команды определяются в свойстве **RoleDefinitions**[файла конфигурации сеанса](session-configurations.md), который использовался для регистрации конечной точки. Вы можете оценить сопоставления ролей в зарегистрированной конечной точке JEA, развернув данные в свойстве **RoleDefinitions**.

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{
  Name = 'Role Capabilities'
  Expression = { $_.Value.RoleCapabilities }
}
```

## <a name="find-available-role-capabilities-on-the-machine"></a>Поиск доступных возможностей ролей на компьютере

JEA получает возможности ролей из `.psrc`-файлов, хранящихся в папке **RoleCapabilities** внутри модуля PowerShell. Следующая функция находит все возможности ролей, доступные на компьютере.

```powershell
function Find-LocalRoleCapability {
    $results = @()

    # Find modules with a "RoleCapabilities" subfolder and add any PSRC files to the result set
    Get-Module -ListAvailable | ForEach-Object {
        $psrcpath = Join-Path -Path $_.ModuleBase -ChildPath 'RoleCapabilities'
        if (Test-Path $psrcpath) {
            $results += Get-ChildItem -Path $psrcpath -Filter *.psrc
        }
    }

    # Format the results nicely to make it easier to read
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{
        Name = 'Path'; Expression = { $_.FullName }
    } | Sort-Object Name
}
```

> [!NOTE]
> Порядок результатов, получаемых из этой функции, необязательно соответствует порядку, в котором будут выбираться возможности ролей, когда несколько возможностей ролей имеют одинаковые имена.

## <a name="check-effective-rights-for-a-specific-user"></a>Проверка действующих прав для конкретного пользователя

Командлет [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) перечисляет все команды, доступные на конечной точке JEA, в зависимости от членства пользователя в группах.
Выходные данные `Get-PSSessionCapability` идентичны данным для указанного пользователя, запустившего `Get-Command -CommandType All` в сеансе JEA.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Если пользователи не являются постоянными членами групп, предоставляющих им дополнительные права JEA, этот командлет может не отражать такие дополнительные разрешения. Такое происходит, когда с помощью систем управления привилегированным доступом JIT реализуется временная принадлежность пользователей к группе безопасности. Тщательно оцените сопоставление пользователей с ролями и возможностями, чтобы убедиться, что пользователи получают только уровень доступа, необходимый для успешного выполнения поставленных задач.

## <a name="powershell-event-logs"></a>Журналы событий PowerShell

Если в системе включено ведение журнала для модуля или блока сценария, в журнале событий Windows можно найти события для каждой команды, которую пользователь выполнял в своих сеансах JEA. Чтобы найти эти события, откройте журнал событий **Microsoft-Windows-PowerShell/Operational** и найдите события с идентификатором **4104**.

Каждая запись журнала событий содержит сведения о сеансе, в котором была запущена команда. Для сеансов JEA событие включает сведения о **ConnectedUser** и **RunAsUser**. **ConnectedUser** является фактическим пользователем, создавшим сеанс JEA. Учетная запись **RunAsUser** используется JEA для выполнения команды.

Журналы событий приложений показывают изменения, внесенные от имени **RunAsUser**. Поэтому включение журнала модулей и скриптов является обязательным для трассировки вызова определенных команд обратно к **ConnectedUser**.

## <a name="application-event-logs"></a>Журналы событий приложений

Команды, которые выполняются в рамках сеанса JEA и взаимодействуют с внешними приложениями или службами, могут записывать события в собственные журналы. В отличие от журналов и записей PowerShell, другие механизмы ведения журнала не записывают действия подключенного пользователя сеанса JEA. Вместо этого эти приложения записывают только виртуальную учетную запись пользователя запуска от имени.
Чтобы определить, кем выполнена команда, требуется просмотреть [запись сеанса](#session-transcripts) или сопоставлять журналы событий PowerShell с временем и пользователем, указанными в журнале событий приложений.

Журнал WinRM может помочь сопоставить пользователей, от имени которых выполняется запуск, в журнале событий приложения с подключающимся пользователем. Событие с идентификатором **193** в журнале **Microsoft-Windows-Windows Remote Management/Operational** регистрирует идентификатор безопасности (SID) и имя учетной записи как для подключающегося пользователя, так и для пользователя, от имени которого выполняется запуск, при каждом создании сеанса JEA.

## <a name="session-transcripts"></a>Записи сеансов

Если вы настроили JEA для создания записи для каждого сеанса пользователя, в указанной папке будет храниться текстовая копия перечня всех действий каждого пользователя.

Следующая команда (от имени администратора) находит все каталоги записей.

```powershell
Get-PSSessionConfiguration |
  Where-Object { $_.TranscriptDirectory -ne $null } |
    Format-Table Name, TranscriptDirectory
```

Каждая запись начинается со сведений о том, когда запущен сеанс, какой пользователь подключился к нему и какое удостоверение JEA было им присвоено.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

В основной части записи регистрируются сведения о каждой из вызванных пользователем команд. Точный синтаксис команды, использованной в сеансах JEA, недоступен из-за способа преобразования команд для удаленного взаимодействия PowerShell. Тем не менее, все же можно определить, какая была выполнена команда. Ниже приведен пример фрагмента записи для пользователя, запускающего `Get-Service Dns` в сеансе JEA:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

Строка **CommandInvocation** записывается для каждой команды, которую запускает пользователь. В **ParameterBindings** записывается каждый параметр и значение, указанное с помощью команды. В приведенном выше примере можно заметить, что параметр **Name** получил значение **Dns** для командлета `Get-Service`.

Выходные данные каждой команды также вызывают **CommandInvocation**, обычно `Out-Default`. **InputObject** в `Out-Default` представляет собой объект PowerShell, возвращаемый из команды. Сведения об этом объекте выводятся несколькими строчками ниже, в точности имитируя то, что увидел бы пользователь.

## <a name="see-also"></a>См. также

[Запись блога *PowerShell ♥ the Blue Team* по безопасности](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
