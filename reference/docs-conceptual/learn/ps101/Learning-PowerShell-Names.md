---
ms.date: 08/24/2018
keywords: powershell,командлет
title: Изучение имен команд PowerShell
ms.openlocfilehash: a65ffcdca6510093b0a77234e20546b6cc1f02bf
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809510"
---
# <a name="learning-powershell-command-names"></a>Изучение имен команд PowerShell

Изучение имен команд и параметров в большинстве интерфейсов командной строки занимает много времени. Проблема в малом числе шаблонов. Запоминание — единственный способ изучить часто используемые команды и параметры.

При освоении новых команд или параметров не всегда получается использовать имеющиеся знания. Вам нужно найти и запомнить новые имена. Как правило, интерфейсы командной строки изначально имеют небольшой набор инструментов, который со временем увеличивается. Это объясняет, почему у них нет стандартизированной структуры.
То же касается и имен команд, так как каждая команда — это отдельный инструмент. В PowerShell реализован более удобный подход к использованию имен команд.

## <a name="learning-command-names-in-traditional-shells"></a>Изучение имен команд в традиционных оболочках

Большинство команд создано для управления элементами операционной системы или приложений, такими как службы или процессы. Имена команд могут относится к семейству команд, а могут и не относиться. Например, в системах Windows можно использовать команды `net start` и `net stop` для запуска и остановки службы. **SC.exe** — еще одно средство управления службами Windows. Это имя не подчиняется шаблону именования команд службы **net.exe**. Для управления процессами в Windows есть команда **tasklist.exe**, которая отображает список процессов, и **taskkill.exe**, которая завершает процессы.

У этих команд нестандартные спецификации параметров. Команду `net start` нельзя использовать для запуска службы на удаленном компьютере, тогда как команда **sc.exe** выполняет эту задачу. При этом необходимо указать удаленный компьютер, задав его имя после двойной обратной косой черты. Чтобы запустить службу очереди печати на удаленном компьютере с именем DC01, введите `sc.exe \\DC01 start spooler`.
Чтобы отобразить список задач, выполняющихся на DC01, введите **/S** и имя компьютера без двойной обратной косой черты. Например, `tasklist /S DC01`.

> [!NOTE]
> До выхода PowerShell версии 6 `sc` было принято использовать как псевдоним командлета `Set-Content`. Таким образом, для запуска команды **sc.exe** в PowerShell версии 6 и ниже необходимо включить полное имя файла **sc.exe** (включая расширение **exe**).

Службы и процессы — это примеры управляемых элементов на компьютере, которые имеют четко определенный жизненный цикл. Вы может запускать или останавливать службы и процессы, а также отображать список всех выполняющихся в данный момент служб и процессов. Несмотря на существенные технические различия между отдельными службами и процессами, действия, которые вы совершаете с ними, по сути одинаковы. Более того, варианты настройки действий с использованием параметров также могут быть похожими.

PowerShell использует это преимущество, чтобы уменьшить число имен, изучаемых для работы с командлетами.

## <a name="cmdlets-use-verb-noun-names-to-reduce-command-memorization"></a>Связка "глагол — существительное" в именах командлетов облегчает запоминание команд

PowerShell использует в именах связку "глагол — существительное". Имя каждого командлета состоит из стандартного глагола и определенного существительного, разделенных дефисом. Используемые в PowerShell глаголы (не только английские) выражают определенное действие. Имена существительные также используются как и в любом языке. Они описывают объекты определенных типов, требуемые для системного администрирования. Приведенные ниже примеры демонстрируют, насколько такие парные имена облегчают запоминание.

В PowerShell есть рекомендуемый список стандартных глаголов. Использование существительных не так ограничено, но они всегда должны обозначать объекты, на которые направлено действие глагола. Вот примеры команд PowerShell: `Get-Process`, `Stop-Process`, `Get-Service`, `Stop-Service`.

В этом примере с парами существительных и глаголов согласованность не слишком упрощает запоминание. Но расширьте этот список до десяти глаголов и десяти существительных и вам придется запомнить всего 20 слов.
Комбинирование этих 20 слов дает 100 разных имен команд.

О функциях команды PowerShell несложно догадаться из ее имени. Команда завершения работы компьютера называется `Stop-Computer`. Команда отображения списка всех компьютеров в сети называется `Get-Computer`. Команда отображения системной даты называется `Get-Date`.

Можно отобразить список всех команд, содержащих определенный глагол, задав параметр **Verb** для команды `Get-Command`. Например, для вывода списка всех командлетов, в которых используется глагол `Get`, введите:

```
PS> Get-Command -Verb Get

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Acl                         Get-Acl [[-Path] <String[]>]...
Cmdlet          Get-Alias                       Get-Alias [[-Name] <String[]...
Cmdlet          Get-AuthenticodeSignature       Get-AuthenticodeSignature [-...
Cmdlet          Get-ChildItem                   Get-ChildItem [[-Path] <Stri...
...
```

Задайте параметр **Noun**, чтобы просмотреть семейство команд, влияющих на объекты одного типа. Например, выполните следующую команду, чтобы просмотреть все команды для управления службами:

```
PS> Get-Command -Noun Service

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Service                     Get-Service [[-Name] <String...
Cmdlet          New-Service                     New-Service [-Name] <String>...
Cmdlet          Restart-Service                 Restart-Service [-Name] <Str...
Cmdlet          Resume-Service                  Resume-Service [-Name] <Stri...
Cmdlet          Set-Service                     Set-Service [-Name] <String>...
Cmdlet          Start-Service                   Start-Service [-Name] <Strin...
Cmdlet          Stop-Service                    Stop-Service [-Name] <String...
Cmdlet          Suspend-Service                 Suspend-Service [-Name] <Str...
...
```

## <a name="cmdlets-use-standard-parameters"></a>Командлеты используют стандартные параметры

Как отмечалось ранее, команды, используемые в распространенных интерфейсах командной строки не всегда имеют согласованные имена параметров. Имена параметров часто состоят из одного символа или аббревиатуры. Их удобно вводить, но сложно понять новым пользователям.

В отличие от большинства других распространенных интерфейсов командной строки PowerShell обрабатывает параметры непосредственно. Наряду с руководством для разработчиков это позволяет стандартизировать имена параметров. Так как это руководство содержит рекомендации, не командлеты будут унифицированными.

Разделитель параметров в PowerShell также является стандартным. В команде PowerShell имени параметра всегда предшествует символ дефиса (-). Рассмотрим следующий пример:

```powershell
Get-Command -Name Clear-Host
```

Имя параметра — это **Name**. Чтобы использовать такой параметр в командной строке, мы введем `-Name`.

Далее приводятся некоторые из общих характеристик обычных имен параметров и использования этих параметров.

### <a name="the-help-parameter-"></a>Параметр справки: Help, ?

Задав параметр `-?` в любом командлете PowerShell, можно получить справку по этому командлету.
При этом командлет не выполняется.

### <a name="common-parameters"></a>Общие параметры

В PowerShell есть несколько *общих параметров*. Эти параметры интерпретируются непосредственно модулем PowerShell. Общие параметры интерпретируются одинаково в любом командлете. Общие параметры — это **WhatIf**, **Confirm**, **Verbose**, **Debug**, **Warn**, **ErrorAction**, **ErrorVariable**, **OutVariable** и **OutBuffer**.

### <a name="recommended-parameter-names"></a>Рекомендуемые имена параметров

Интегрированные в PowerShell командлеты используют унифицированные имена для схожих параметров. Использование таких имен не является обязательным, но в руководстве явно рекомендуется соблюдать согласованность.

Например, рекомендуемое имя параметра, который ссылается на компьютер, — это **ComputerName**, а не Server, Host, System, Node или другие распространенные варианты. В числе других настоятельно рекомендуемых имен параметров — **Force**, **Exclude**, **Include**, **PassThru**, **Path** и **CaseSensitive**.