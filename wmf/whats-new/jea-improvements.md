---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
title: Улучшения Just Enough Administration (JEA)
ms.openlocfilehash: 847ae92a6225023bcd0ee3dfe7c7058bdc356836
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65855489"
---
# <a name="improvements-to-just-enough-administration-jea"></a>Улучшения Just Enough Administration (JEA)

Just Enough Administration — это новая функция в WMF 5.0, позволяющая осуществлять ролевое администрирование через удаленное взаимодействие PowerShell. Она расширяет существующую инфраструктуру ограниченных конечных точек, позволяя пользователям, которые не являются администраторами, выполнять определенные команды, скрипты и исполняемые файлы с правами администратора. Это помогает уменьшить число полных администраторов в среде и повысить безопасность.

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a>Ограниченное копирование файлов в конечные точки JEA и из них

Теперь вы можете удаленно копировать файлы в конечную точку JEA и из нее, не беспокоясь о том, что подключающийся пользователь сможет скопировать *любой* файл в вашей системе. Это возможно благодаря настройке подключения диска пользователя в PSSC-файле. Диск пользователя — это новый PSDrive, уникальный для каждого подключающегося пользователя; он сохраняется между сеансами. Когда для копирования файлов в сеанс JEA или из него используется `Copy-Item`, доступ разрешен только на диск пользователя. Копировать файлы на другой PSDrive будет невозможно.

Чтобы настроить диск пользователя в файле конфигурации сеанса JEA, используйте следующие новые поля.

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

Папка с резервной копией диска пользователя будет создана здесь: `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`.

Чтобы использовать диск пользователя и копировать файлы в конечную точку JEA с доступом к диску пользователя и из нее, используйте параметры `-ToSession` и `-FromSession` в `Copy-Item`.

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine.
# You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

Затем вы сможете записать пользовательские функции для обработки данных, хранящихся на диске пользователя, и предоставить их пользователям в файле возможностей ролей.

## <a name="support-for-group-managed-service-accounts"></a>Поддержка групповых учетных записей управляемой службы

В некоторых случаях для выполнения задачи пользователем в сеансе JEA может потребоваться доступ к ресурсам за пределами локального компьютера. Если в сеансе JEA настроено использование виртуальной учетной записи, любые попытки подключиться к таким ресурсам будут отображаться как полученные из удостоверения локального компьютера, а не из виртуальной учетной записи или от подключенного пользователя. В TP5 включена поддержка работы JEA в контексте [групповой управляемой учетной записи службы](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), что значительно облегчает доступ к сетевым ресурсам с использованием идентификатора домена.

Чтобы настроить работу сеанса JEA в учетной записи gMSA, используйте следующий новый ключ в PSSC-файле:

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> Групповые управляемые учетные записи службы не допускают изоляцию или ограниченную область виртуальных учетных записей.
> Каждый подключающийся пользователь будет иметь такое удостоверение gMSA, у которого могут быть разрешения во всей организации. Будьте внимательны при использовании gMSA. По возможности всегда рекомендуется использовать виртуальные учетные записи, действующие на локальном компьютере.

## <a name="conditional-access-policies"></a>Политики условного доступа

JEA отлично подходит для ограничения действий управления при подключении к системе, но что, если вы также хотите ограничить *время* использования JEA? Мы добавили варианты настройки в файлы конфигурации сеанса (PSSC), чтобы вы могли указать группы безопасности, к которым должен принадлежать пользователь для запуска сеанса JEA. Это может быть особенно полезным, если в вашей среде установлена система Just In Time (JIT) и вам нужно, чтобы пользователи повышали свои права перед доступом к привилегированной конечной точке JEA.

Новое поле *RequiredGroups* в PSSC-файле позволяет указать, может ли пользователь подключиться к JEA. Логика состоит в указании хэш-таблицы (при необходимости вложенной), которая использует ключи And и Or для создания правил. Ниже представлены примеры использования этого поля.

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a>Исправлено: виртуальные учетные записи теперь поддерживаются в Windows Server 2008 R2

Теперь в WMF 5.1 вы можете использовать виртуальные учетные записи в Windows Server 2008 R2, включив согласованные конфигурации и паритет функций в Windows Server 2008 R2 — 2016. Виртуальные учетные записи по-прежнему не поддерживаются при использовании JEA в Windows 7.