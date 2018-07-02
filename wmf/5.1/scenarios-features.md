---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,установка
title: Новые сценарии и возможности в WMF 5.1
ms.openlocfilehash: b00069aad7422f86d1462a62a6c4bc8a91e46705
ms.sourcegitcommit: 50b66cada6943784b8d3c103cebc3c1e3e286a16
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090369"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a>Новые сценарии и возможности в WMF 5.1

> Примечание. Эта информация является предварительной и может быть изменена.

## <a name="powershell-editions"></a>Выпуски PowerShell

Начиная с версии 5.1, среда PowerShell доступна в разных выпусках, обладающих различными наборами функций и совместимостью с платформами.

- **Выпуск Desktop Edition:** построен на основе .NET Framework и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в полноценных выпусках Windows, таких как Server Core и Windows Desktop.
- **Выпуск Core Edition:** построен на основе .NET Core и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в выпусках Windows с ограниченными возможностями, таких как Nano Server и Windows IoT.

**Дополнительные сведения об использовании выпусков PowerShell**

- [Определение запущенного выпуска PowerShell с использованием $PSVersionTable](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [Фильтрация результатов командлета Get-Module по CompatiblePSEditions с помощью параметра PSEdition](/powershell/module/microsoft.powershell.core/get-module)
- [Запрет на выполнение сценариев в несовместимых выпусках PowerShell](/powershell/gallery/concepts/script-psedition-support)
- [Объявление совместимости модуля с определенными версиями PowerShell](/powershell/gallery/concepts/module-psedition-support)

## <a name="catalog-cmdlets"></a>Командлеты для работы с каталогами

Мы добавили два новых командлета для создания и проверки файлов каталога Windows в модуль [Microsoft.Powershell.Security](/powershell/module/microsoft.powershell.security).

### <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

Командлет New-FileCatalog создает файл каталога Windows для набора файлов и папок.
Файл каталога содержит хэши для всех файлов, находящихся по указанным путям.
Пользователь может распространять набор папок вместе с соответствующим файлом каталога, представляющим этих папки.
С помощью файла каталога получатель может проверить, были ли изменены папки с момента создания каталога.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Поддерживаются каталоги версий 1 и 2.
В версии 1 для создания хэшей файлов используется алгоритм хэширования SHA1, в версии 2 — SHA256.
Каталог версии 2 не поддерживается в *Windows Server 2008 R2* и *Windows 7*.
На платформах *Windows 8*, *Windows Server 2012* и более поздней версии рекомендуется использовать каталог версии 2.

![](../images/NewFileCatalog.jpg)

Следующая команда создает файл каталога.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Для проверки целостности файла каталога (Pester.cat в приведенном выше примере) его нужно подписать с помощью командлета [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature).

### <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

Командлет Test-FileCatalog проверяет каталог, представляющий набор папок.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Этот командлет сравнивает все хэши файлов и их относительные пути в *каталоге* с хэшами и относительными путями на *диске*.
При обнаружении любого несоответствия между хэшами файлов и путями он возвращает состояние *ValidationFailed*.
Все эти данные можно получить с помощью параметра *-Detailed*.
Командлет также отображает состояние подписи каталога в свойстве *Signature*. Подпись также можно определить, вызвав командлет [Get-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Get-AuthenticodeSignature) и указав файл каталога.
Также можно исключить любые файлы из проверки, указав их в параметре *-FilesToSkip*.

## <a name="module-analysis-cache"></a>Кэш анализа модуля

Начиная с версии WMF 5.1 среда PowerShell предоставляет средства управления файлом, в котором кэшируются сведения о модуле, например экспортируемые им команды.

По умолчанию этот кэш хранится в файле `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
Кэш обычно считывается при запуске в процессе поиска команды и записывается в фоновом потоке через некоторое время после импорта модуля.

Чтобы изменить расположение кэша по умолчанию, присвойте значение переменной среды `$env:PSModuleAnalysisCachePath` перед запуском PowerShell.
Изменения, вносимые в эту переменную среды, влияют только на дочерние процессы.
Значение должно быть полным путем (включая имя файла), на создание и запись файлов по которому у среды PowerShell есть разрешение.
Чтобы отключить файловый кэш, укажите в качестве этого значения недопустимое расположение, например:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Таким образом задается путь к недопустимому устройству.
Если среда PowerShell не может осуществлять запись по указанному пути, ошибка не выводится; сообщения об ошибках можно получить, используя трассировщик:

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

При выгрузке кэша среда PowerShell ищет модули, которые больше не существуют, чтобы кэш не был излишне большим.
Иногда эти проверки нежелательны. В этом случае их можно отключить, задав

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

Новое значение этой переменной среды вступает в силу немедленно в текущем процессе.

## <a name="specifying-module-version"></a>Указание версии модуля

В WMF 5.1 `using module` работает так же, как другие связанные с модулями конструкции в PowerShell.
Ранее не было возможности указать определенную версию модуля; при наличии нескольких версий возникала ошибка.

В WMF 5.1:

- Вы можете использовать [конструктор ModuleSpecification (Hashtable)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).
Она имеет тот же формат, что и `Get-Module -FullyQualifiedName`.

**Пример:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- Если имеется несколько версий модуля, в PowerShell используется **та же логика разрешения**, что и в `Import-Module`, и ошибка не выводится. Это поведение аналогично поведению `Import-Module` и `Import-DscResource`.

## <a name="improvements-to-pester"></a>Усовершенствования Pester

В WMF 5.1 версия Pester, распространяемая с PowerShell, была обновлена с 3.3.5 до 3.4.0. Также в репозиторий было добавлено изменение https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, которое улучшает работу Pester с Nano Server.

Чтобы просмотреть изменения в версиях с 3.3.5 по 3.4.0, откройте файл ChangeLog.md: https://github.com/pester/Pester/blob/master/CHANGELOG.md
