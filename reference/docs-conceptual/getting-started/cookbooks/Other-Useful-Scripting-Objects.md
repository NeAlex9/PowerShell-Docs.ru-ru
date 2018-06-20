---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Другие полезные объекты для сценариев
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 0e87e9919199e011ab5abec5b07dccc8494ad64a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949831"
---
# <a name="other-useful-scripting-objects"></a>Другие полезные объекты для сценариев

Следующие объекты предоставляют дополнительные возможности создания сценариев в интегрированной среде сценариев Windows PowerShell. Они не являются частью иерархии **$psISE**.

## <a name="useful-scripting-objects"></a>Полезные объекты для сценариев

### <a name="psunsupportedconsoleapplications"></a>$psUnsupportedConsoleApplications

Существуют некоторые ограничения, применяемые к взаимодействию интегрированной среды сценариев Windows PowerShell с консольными приложениями. Команда или сценарий автоматизации, требующие участия пользователя, могут не работать так, как при запуске из консоли Windows PowerShell. Может потребоваться заблокировать запуск этих команд или сценариев в области команд интегрированной среды сценариев Windows PowerShell. Объект **$PsUnsupportedConsoleApplications** хранит список таких команд. При попытке выполнить команды, указанные в этом списке, вы получите сообщение о том, что они не поддерживаются. Следующий сценарий добавляет запись в этот список.

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a>$psLocalHelp

Это объект словаря, который поддерживает сопоставление с учетом контекста разделов справки и связанных ссылок в локальном скомпилированном файле справки HTML. Он используется для поиска локальной справки для определенного раздела. Разделы в этом списке можно добавлять и удалять. В следующем примере кода показаны некоторые примеры пар "ключ —значение", которые содержатся в объекте **$psLocalHelp**.

```powershell
# See the local help map
$psLocalHelp | Format-List
```

### <a name="sample-output"></a>Пример вывода

|||
|-|-|
|Ключ: Add-Computer|Значение: WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm|
|Ключ: Add-Content|Значение: WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm|

Следующий сценарий добавляет запись в этот список.

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a>$psOnlineHelp

Это объект словаря, который поддерживает сопоставление с учетом контекста заголовков разделов справки и связанных внешних URL-адресов. Он используется для поиска справки для определенного раздела в Интернете. Разделы в этом списке можно добавлять и удалять.

```powershell
$psOnlineHelp | Format-List
```

### <a name="sample-output"></a>Пример вывода

|||
|-|-|
|Ключ: Add-Computer|Значение: http://go.microsoft.com/fwlink/p/?LinkID=135194|
|Ключ: Add-Content|Значение: http://go.microsoft.com/fwlink/p/?LinkID=113278|

 Следующий сценарий добавляет запись в этот список.

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a>См. также

- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)