---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,установка
title: Исправления ошибок в WMF 5.1
ms.openlocfilehash: 1e46d6d0419b3497450e6eaddbaa47456b004691
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
---
# <a name="bug-fixes-in-wmf-51"></a>Исправления ошибок в WMF 5.1#

## <a name="bug-fixes"></a>Устранение ошибок ##

В WMF 5.1 исправлены следующие важные ошибки.

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a>При автоматическом обнаружении модулей полностью учитывается `$env:PSModulePath`. ###

Автоматическое обнаружение модулей (их автоматическая загрузка без явного вызова Import-Module при вызове команды) появилось в WMF 3.
В этой версии среда PowerShell проверяла команды в `$PSHome\Modules` перед использованием `$env:PSModulePath`.

В WMF 5.1 это поведение изменилось: `$env:PSModulePath` учитывается полностью.
Это позволяет автоматически загружать созданные пользователями модули, в которых определяются предоставляемые PowerShell команды (например, `Get-ChildItem`), и правильно переопределять встроенные команды.

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a>При перенаправлении файлов больше не задается жестко `-Encoding Unicode`. ###

Во всех предыдущих версиях PowerShell было невозможно контролировать кодировку файлов, используемую оператором перенаправления файлов, например `Get-ChildItem > out.txt`, так как среда PowerShell добавляла параметр `-Encoding Unicode`.

Начиная с версии WMF 5.1 можно изменять кодировку файлов при перенаправлении, задавая `$PSDefaultParameterValues`:

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a>Исправлена регрессия при доступе к членам `System.Reflection.TypeInfo`. ###

Появившаяся в WMF 5.0 регрессия нарушала доступ к членам `System.Reflection.RuntimeType`, например `[int].ImplementedInterfaces`.
Эта ошибка исправлена в WMF 5.1.


### <a name="fixed-some-issues-with-com-objects"></a>Исправлены некоторые проблемы с объектами COM ###

В WMF 5.0 появился новый модуль привязки COM для вызова методов применительно к COM-объектам и доступа к свойствам COM-объектов.
Этот новый модуль значительно повысил производительность, но в нем был ряд ошибок, которые исправлены в WMF 5.1.

#### <a name="argument-conversions-were-not-always-performed-correctly"></a>Преобразование аргументов не всегда выполнялось правильно ####

Рассмотрим следующий пример:

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

Метод SendKeys требует строку, но среда PowerShell не преобразовала char в string, отложив преобразование до вызова метода IDispatch::Invoke, который использует VariantChangeType для выполнения преобразования. В этом примере это приводит к отправке ключей "1", "7" и "3" вместо требуемого ключа Volume.Mute.

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a>Перечисляемые COM-объекты не всегда обрабатывались правильно ####

Среда PowerShell, как правило, перечисляет большинство перечисляемых объектов, но регрессия, появившаяся в WMF 5.0, препятствовала перечислению COM-объектов, реализующих интерфейс IEnumerable.  Например:

```
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

В приведенном выше примере WMF 5.0 записывает Scripting.Dictionary в конвейер (что неправильно) вместо перечисления пар "ключ-значение".

Это изменение также устраняет [проблему 1752224 (о которой было сообщено через Connect)](https://connect.microsoft.com/PowerShell/feedback/details/1752224).

### <a name="ordered-was-not-allowed-inside-classes"></a>`[ordered]` не разрешалось использовать в классах. ###

В WMF 5.0 появились классы, в которых проверялось использование литералов типов.
`[ordered]` выглядит как литерал типа, но в действительности не является типом .NET.
В WMF 5.0 ошибочно выдавалась ошибка для `[ordered]` внутри класса:

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a>Вызов разделов справки при наличии нескольких версий не работал ###

До версии WMF 5.1 при наличии нескольких установленных версий модуля с общим разделом справки, например "about_PSReadline", команда `help about_PSReadline` возвращала несколько разделов без возможности просмотреть саму справку.

В WMF 5.1 эта проблема устранена: теперь возвращается последняя версия раздела.

`Get-Help` не позволяет указать версию, по которой требуется справка.
В качестве обходного решения можно перейти к каталогу модулей и открыть справку напрямую, например с помощью любимого редактора.

### <a name="powershellexe-reading-from-stdin-stopped-working"></a>Программа powershell.exe, считывающая данные из STDIN, прекратила работу.

Клиенты используют `powershell -command -` в приложениях в машинном коде для передачи скрипта PowerShell с помощью STDIN. Теперь это невозможно из-за других изменений в узле консоли.

https://windowsserver.uservoice.com/forums/301869-powershell/suggestions/15854689-powershell-exe-command-is-broken-on-windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a>Программа powershell.exe создает пик загрузки ЦП при запуске.

PowerShell использует запрос WMI, чтобы проверить, запущен ли он с помощью групповой политики, чтобы избежать задержки входа.
Запрос WMI завершается вставкой tzres.mui.dll в каждый процесс в системе, так как класс Win32_Process WMI пытается извлечь сведения о локальном часовом поясе.
Это приводит к пику загрузки ЦП в wmiprvse (узел поставщика WMI).
Чтобы исправить это, используйте вызовы API Win32 вместо WMI, чтобы получить те же сведения.
