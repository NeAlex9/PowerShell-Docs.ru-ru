---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 5ac9566979e1b761249f5cc7c62ed44047a2b9f6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058018"
---
# <a name="register-a-powershell-repository"></a>Регистрация репозитория PowerShell
Вы можете настроить работу PowerShellGet с внутренними репозиториями. Для этого были добавлены следующие компоненты.
- Register-PSRepository: регистрирует репозиторий для текущего пользователя.
- Unregister-PSRepository: удаляет зарегистрированный репозиторий для текущего пользователя.
- Set-PSRepository: задает значения для зарегистрированного репозитория.
- Get-PSRepository: возвращает все зарегистрированные репозитории для текущего пользователя.

После регистрации репозитория командлеты Find-Module и Install-Module можно настроить на работу с ним.

```powershell
\#Register a default repository
Register-PSRepository –Name DemoRepo –SourceLocation “https://www.myget.org/F/powershellgetdemo/api/v2” –PublishLocation “<https://www.myget.org/F/powershellgetdemo/api/v2>/package” –InstallationPolicy –Trusted

\#Get all of the registered repositories
Get-PSRepository
Name SourceLocation
---- --------------
PSGallery https://msconfiggallery.cloudapp...
DemoRepo https://www.myget.org/F/powershe...

\#Search only the new repository for modules
Find-Module -Repository DemoRepo
Repository Version Name
---------- ------- ----
DemoRepo 1.0.1 xActiveDirectory
DemoRepo 1.1.1 SomeModule

\#By default, PowerShellGet operates against all registered repositories when none is specified. In this example, the “SomeModule” module is installed from the DemoRepo.
Install-Module SomeModule

\#Removing a repository
Unregister-PSRepository DemoRepo
```
