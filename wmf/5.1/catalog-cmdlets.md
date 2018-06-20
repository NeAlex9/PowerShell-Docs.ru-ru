---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,установка
title: Командлеты для работы с каталогами
ms.openlocfilehash: 7eaca09667af0eb5d719f23e987bb112e8514978
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189073"
---
# <a name="catalog-cmdlets"></a>Командлеты для работы с каталогами

Мы добавили два новых командлета для создания и проверки файлов каталога Windows в модуль [Microsoft.Powershell.Security](https://technet.microsoft.com/en-us/library/hh847877.aspx).

## <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

`New-FileCatalog` создает файл каталога Windows для набора файлов и папок. Файл каталога содержит хэши для всех файлов, находящихся по указанным путям. Пользователь может распространять набор папок вместе с соответствующим файлом каталога, представляющим этих папки. Файл каталога может использоваться получателем содержимого, чтобы проверить, были ли внесены изменения в папки после создания каталога.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
Поддерживается создание каталогов версий 1 и 2. В версии 1 для создания хэшей файлов используется алгоритм хэширования SHA1, в версии 2 — SHA256. Каталог версии 2 не поддерживается в *Windows Server 2008 R2* и *Windows 7*. На платформах *Windows 8* и *Windows Server 2012* и более поздней версии рекомендуется использовать каталог версии 2.

Для использования этой команды в существующем модуле укажите для переменных CatalogFilePath и Path значения, соответствующие расположению манифеста модуля. В следующем примере манифест модуля располагается в папке "C:\Program Files\Windows PowerShell\Modules\Pester".

![](../images/NewFileCatalog.jpg)

Следующая команда создает файл каталога.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Для проверки целостности файла каталога (Pester.cat в примере выше) его нужно подписать командлетом [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).


## <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

`Test-FileCatalog` проверяет каталог, представляющий набор папок.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Этот командлет сравнивает хэши всех файлов и их относительные пути, найденные в файле каталога, с сохраненными на жестком диске. При обнаружении любого несоответствия между хэшами файлов и путями он возвращает состояние `ValidationFailed`.
Все эти данные можно получить при помощи флага `Detailed`. Состояние подписанности каталога отображается в поле `Signature`. Подпись также можно определить, вызвав командлет [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) и указав файл каталога.
Также можно исключить любые файлы из проверки, указав их в параметре `FilesToSkip`.
