---
ms.date: 06/12/2017
contributor: manikb
keywords: коллекция,powershell,командлет,psget
title: Начальная загрузка поставщика NuGet
ms.openlocfilehash: 6d8f106bc3b8741203e87e4c097948a843f06d6e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084391"
---
# <a name="bootstrap-the-nuget-provider-and-nugetexe"></a>Начальная загрузка поставщика NuGet и NuGet.exe

Файл NuGet.exe включен в последний поставщик NuGet. Для операций публикации модулей или скриптов PowerShellGet требуется двоичный исполняемый файл NuGet.exe. Для всех других операций, включая *поиск*, *установку*, *сохранение* и *удаление*, требуется только поставщик NuGet.
PowerShellGet содержит логику обработки совместной начальной загрузки поставщика NuGet и NuGet.exe или начальной загрузки только поставщика NuGet. В любом случае должно появиться только одно сообщение запроса. Если компьютер не подключен к Интернету, пользователь или администратор должен скопировать на него доверенный экземпляр поставщика NuGet и/или файл NuGet.exe.

> [!NOTE]
> Начиная с версии 6, поставщик NuGet содержится в установке PowerShell.

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a>Устранение ошибки, при которой поставщик NuGet не устанавливается на автономный компьютер

```powershell
Find-Module -Repository PSGallery -Verbose -Name Contoso
```

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n
Find-Module : NuGet provider is required to interact with NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed.
At line:1 char:1
+ Find-Module -Repository PSGallery -Verbose -Name Contoso
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Find-Module], InvalidOperationException
   + FullyQualifiedErrorId : CouldNotInstallNuGetProvider,Find-Module
```

```powershell
Find-Module -Repository PSGallery -Verbose -Name Contoso
```

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
2.5        Contoso                             Module     PSGallery        Contoso module
```

## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Устранение ошибки, при которой во время операции публикации на автономном компьютере доступен поставщик NuGet, но недоступен NuGet.exe

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module
```

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Устранение ошибки, при которой во время операции публикации на автономном компьютере недоступны поставщик NuGet и NuGet.exe

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed and NuGet.exe is available under
one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetBinaries,Publish-Module
```

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a>Ручной режим начальной загрузки поставщика NuGet на автономный компьютер

В указанных выше случаях предполагается, что компьютер подключен к Интернету и может скачать файлы из общедоступного расположения. Если это невозможно, единственным вариантом является начальная загрузка на компьютере с помощью процессов, приведенных выше, и ручное копирование поставщика на изолированный узел с помощью автономного доверенного процесса. Наиболее распространенный случай использования такого сценария — это когда частная коллекция доступна для поддержки изолированной среды.

После выполнения перечисленных выше процедур для начальной загрузки компьютера, подключенного к Интернету, вы увидите файлы поставщика в расположении:

`C:\Program Files\PackageManagement\ProviderAssemblies\`

Структура папок или файлов поставщика NuGet будет следующей (возможно, с другим номером версии):

```
NuGet
--2.8.5.208
----Microsoft.PackageManagement.NuGetProvider.dll
```

Скопируйте эти папки и файл с помощью доверенного процесса на автономные компьютеры.

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a>Ручной режим начальной загрузки поставщика NuGet на автономном компьютере для поддержки операций публикации

Если компьютер будет использоваться для публикации модулей или скриптов в частной коллекции с помощью командлетов `Publish-Module` или `Publish-Script`, помимо выполнения начальной загрузки поставщика NuGet вручную потребуется двоичный исполняемый файл NuGet.exe.

Наиболее распространенный случай использования такого сценария — это когда частная коллекция доступна для поддержки изолированной среды. Существует два варианта получения файла NuGet.exe.

Первый вариант — выполнить начальную загрузку на компьютере, подключенном к Интернету, и скопировать файлы на автономные компьютеры с помощью доверенного процесса. После начальной загрузки подключенного к Интернету компьютера двоичный файл NuGet.exe будет находиться в одной из двух папок:

При выполнении командлетов `Publish-Module` или `Publish-Script` с повышенным уровнем разрешений (от имени администратора):

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Если командлеты выполнялись от имени пользователя без разрешения более высокого уровня:

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

Второй вариант — загрузить NuGet.exe с веб-сайта NuGet.Org: [https://dist.nuget.org/index.html](https://www.nuget.org/downloads) При выборе версии для рабочих компьютеров убедитесь, что это версия младше 2.8.5.208, и определите версию с пометкой "рекомендуется". Обязательно разблокируйте файл, если он был скачан с помощью браузера. Это можно сделать с помощью командлета `Unblock-File`.

В любом случае можно скопировать файл NuGet.exe в любое расположение в `$env:path`, но стандартные расположения следующие:

Чтобы сделать исполняемый файл доступным для предоставления всем пользователям возможности применять командлеты `Publish-Module` и `Publish-Script`, используйте следующее:

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Чтобы сделать доступным исполняемый файл только для конкретных пользователей, скопируйте его в расположение профиля только нужного пользователя:

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```
