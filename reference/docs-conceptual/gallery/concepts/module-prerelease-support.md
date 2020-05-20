---
ms.date: 09/26/2017
contributor: keithb
keywords: коллекция,powershell,командлет,psget
title: Предварительные версии модулей
ms.openlocfilehash: eced067dd21082de0db653daf3b838217154f1dd
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "71328145"
---
# <a name="prerelease-module-versions"></a>Предварительные версии модулей

Начиная с версии 1.6.0, PowerShellGet и коллекция PowerShell поддерживают маркировку версий с номерами выше 1.0.0 как предварительных. До этого номера предварительных версий пакетов должны были обязательно начинаться с 0. Такая возможность добавлена, чтобы улучшить поддержку соглашения о версиях [SemVer 1.0.0](http://semver.org/spec/v1.0.0.html) и при этом сохранить обратную совместимость с PowerShell версий 3 и выше, а также с текущими версиями PowerShellGet. Этот раздел описывает особенности присвоения версий модулям. Аналогичные возможности для сценариев см. в разделе [Предварительные версии сценариев](script-prerelease-support.md). Благодаря этой возможности издатель может присвоить своему модулю или сценарию предварительную версию 2.5.0-alpha, а затем выпустить готовую к использованию версию 2.5.0, которая заменит предварительную.

На высоком уровне возможности для предварительных версий модулей включают следующее.

- Добавление строки предварительной версии в раздел PSData манифеста модуля определяет версию модуля как предварительную. При публикации модуля в коллекции PowerShell эти данные извлекаются из манифеста и используются для определения предварительных версий пакетов.
- Для получения предварительных версий пакетов необходимо добавить флаг `-AllowPrerelease` в команды PowerShellGet `Find-Module`, `Install-Module`, `Update-Module` и `Save-Module`. Если этот флаг не указан, предварительные версии не будут отображаться.
- Версии модулей, отображаемые в `Find-Module`,`Get-InstalledModule` и коллекции PowerShell, будут отображаться как одна строка с добавлением строки предварительной версии, например: 2.5.0-alpha.

Ниже приведено подробное описание этих возможностей.

Данные изменения совместимы с PowerShell 3.0, 4.0 и 5 и не влияют на поддержку версий модулей, встроенную в PowerShell.

## <a name="identifying-a-module-version-as-a-prerelease"></a>Определение версии модуля как предварительной

Для использования предварительных версий в PowerShellGet необходимо заполнить два поля в манифесте модуля.

- Версия в поле ModuleVersion манифеста модуля должна состоять из трех частей и соответствовать текущей системе версий PowerShell. Формат версии должен быть вида A.B.C, где A, B и C — целые числа.
- Строка предварительной версии задается в подразделе PSData раздела PrivateData в манифесте модуля.

Ниже приведены подробные требования к строке предварительной версии.

Пример раздела манифеста модуля, определяющего версию модуля как предварительную

```powershell
@{
    ModuleVersion = '2.5.0'
    #---
    PrivateData = @{
        PSData = @{
            Prerelease = 'alpha'
        }
    }
}
```

Подробные требования к строке предварительной версии.

- Строку предварительной версии можно указать, только если версия в поле ModuleVersion состоит из трех сегментов в виде <основная_версия>.<дополнительная_версия>.<сборка>. Это соответствует соглашению о версиях SemVer 1.0.0.
- Разделителем между номером сборки и строкой предварительной версии является дефис. Дефис может включен в строку предварительной версии только как первый символ.
- Строка предварительной версии может содержать только буквенно-цифровые символы ASCII [0-9A-Za-z-]. Рекомендуем начинать эту строку с буквы — так вам будет проще различать предварительные версии при просмотре списка пакетов.
- В настоящий момент поддерживается только SemVer версии 1.0.0. Строка предварительной версии **не должна** содержать ни точек, ни символов + [.+], которые допустимы в SemVer 2.0.
- Пример поддерживаемых строк предварительной версии: -alpha, -alpha1, -BETA, -update20171020

### <a name="prerelease-versioning-impact-on-sort-order-and-installation-folders"></a>Влияние предварительных версий на порядок сортировки и установочные папки

При использовании предварительных версий изменяется порядок сортировки, что имеет значение при публикации сценариев в коллекции PowerShell и при установке модулей с помощью команд PowerShellGet. Если строка предварительной версии задана для двух модулей, то сортировка производится по части строки, следующей после дефиса. Таким образом версия 2.5.0-alpha меньше, чем 2.5.0-beta, а последняя меньше, чем 2.5.0-gamma. Если два модуля обладают одинаковым значением ModuleVersion и только у одного из них есть строка предварительной версии, то готовым к использованию модулем будет считаться модуль без этой строки и при сортировке он будет указываться, как имеющий более высокую версию по отношению к предварительной (включающей строку предварительной версии). Например: при сравнении версий 2.5.0 и 2.5.0-beta, будет считаться, что версия 2.5.0 имеет больший номер.

По умолчанию при публикации в коллекции PowerShell новый модуль обязательно должен иметь более высокую версию, чем все модули, опубликованные ранее.

## <a name="finding-and-acquiring-prerelease-packages-using-powershellget-commands"></a>Поиск и получение предварительных версий пакетов с помощью команд PowerShellGet

Для работы с предварительными версиями пакетов с помощью таких команд PowerShellGet, как Find-Module, Install-Module, Update-Module и Save-Module, необходимо добавлять флаг -AllowPrerelease. Если флаг -AllowPrerelease указан, в результат выполнения команды будут включены доступные предварительные версии пакетов. Если флаг -AllowPrerelease не указан, предварительные версии не будут отображаться.

Единственным исключением является команда Get-InstalledModule и в некоторых случаях команда Uninstall-Module.

- Команда Get-InstalledModule всегда автоматически показывает информацию о предварительных версиях в строке версии для модулей.
- Если __номер версии не указан__, то по умолчанию команда Uninstall-Module удалит самую последнюю версию модуля. Такое поведение команды осталось неизменным. Если в параметре -RequiredVersion указана предварительная версия, то необходимо будет также указать флаг -AllowPrerelease.

## <a name="examples"></a>Примеры

Предположим, что коллекция PowerShell включает модуль TestPackage версий 1.8.0 и 1.9.0-alpha. Если `-AllowPrerelease` не указать, будет возвращена только версия 1.8.0.

```powershell
find-module TestPackage
```

```output
Version        Name           Repository  Description
-------        ----           ----------  -----------
1.8.0          TestPackage    PSGallery   Package used to validate changes to the PowerShe...
```

```powershell
find-module TestPackage -AllowPrerelease
```

```output
Version        Name           Repository  Description
-------        ----           ----------  -----------
1.9.0-alpha    TestPackage    PSGallery   Package used to validate changes to the PowerShe...
```

Чтобы установить предварительный выпуск, всегда указывайте - AllowPrerelease. Просто указать строку предварительной версии будет недостаточно.

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha
```

```output
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exception
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage
```

Предыдущую команду выполнить не удалось, так как не указано - AllowPrerelease. Добавьте `-AllowPrerelease`.

```powershell
Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
Get-InstalledModule TestPackage
```

```output
Version         Name          Repository  Description
-------         ----          ----------  -----------
1.9.0-alpha     TestPackage   PSGallery   Package used to validate changes to the PowerShe...
```

Не поддерживается одновременная установка модулей, версии которых отличаются только значением предварительной версии. При использовании PowerShellGet разные версии одного модуля могут быть установлены одновременно. Каждая из них помещается в папку с именем, использующим значение ModuleVersion. ModuleVersion используется для имени папки без добавления строки предварительной версии. Если пользователь установит модуль MyModule версии 2.5.0-alpha, этот модуль будет помещен в папку `MyModule\2.5.0`. Если пользователь затем установит версию 2.5.0-beta, содержимое папки `MyModule\2.5.0` будет **перезаписано**. Одним из преимуществ такого подхода является то, что нет необходимости удалять предварительную версию после установки версии, готовой к использованию. Пример ниже иллюстрирует работу этого правила.

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
1.9.0-alpha     TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name            Repository  Description
-------        ----            ----------  -----------
1.9.0-beta     TestPackage     PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
1.9.0-beta      TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

```

Если не задан флаг -RequiredVersion, то команда Uninstall-Module удалит самую последнюю версию модуля.
Если в параметре -RequiredVersion указана предварительная версия, то необходимо обязательно добавить к команде флаг -AllowPrerelease.

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name           Repository  Description
-------         ----           ----------  -----------
2.0.0-alpha1    TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.8.0           TestPackage    PSGallery   Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage    PSGallery   Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta

Uninstall-Module : The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Module], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninstall-Module

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name          Repository   Description
-------         ----          ----------   -----------
2.0.0-alpha1    TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.8.0           TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage   PSGallery    Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name          Repository   Description
-------         ----          ----------   -----------
1.8.0           TestPackage   PSGallery    Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage   PSGallery    Package used to validate changes to the PowerShe...
```

## <a name="more-details"></a>Дополнительные сведения

- [Предварительные версии сценариев](script-prerelease-support.md)
- [Find-Module](/powershell/module/powershellget/find-module)
- [Install-Module](/powershell/module/powershellget/install-module)
- [Save-Module](/powershell/module/powershellget/save-module)
- [Update-Module](/powershell/module/powershellget/Update-Module)
- [Get-InstalledModule](/powershell/module/powershellget/get-installedmodule)
- [Uninstall-Module](/powershell/module/powershellget/uninstall-module)
