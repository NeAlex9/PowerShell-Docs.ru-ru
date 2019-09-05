---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Управление дисками Windows PowerShell
ms.openlocfilehash: 5d1aba459caeaab2542e17e74534da6713b0faa9
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215505"
---
# <a name="managing-windows-powershell-drives"></a>Управление дисками Windows PowerShell

*Диск Windows PowerShell* — это расположение хранилища данных, доступ к которому можно получить так же, как к диску файловой системы в Windows PowerShell. Поставщики Windows PowerShell создают несколько дисков, например диски файловой системы (включая C: и D:), диски реестра (HKCU: и HKLM:) и диск сертификата (Cert:), а вы можете создать собственные диски Windows PowerShell. Эти диски очень полезны, но они доступны только в Windows PowerShell. К ним невозможно получить доступ с помощью других средств Windows, например проводника или Cmd.exe.

Windows PowerShell использует существительное **PSDrive** для команд, которые работают на дисках Windows PowerShell. Для получения списка дисков Windows PowerShell в сеансе Windows PowerShell используйте командлет **Get-PSDrive**.

```
PS> Get-PSDrive

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
Alias      Alias
C          FileSystem    C:\                                 ...And Settings\me
cert       Certificate   \
D          FileSystem    D:\
Env        Environment
Function   Function
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
Variable   Variable
```

Хотя отображение дисков в списке зависит от дисков в вашей системе, список будет выглядеть аналогично выходным данным команды **Get-PSDrive**, показанной выше.

Диски файловой системы являются подмножеством дисков Windows PowerShell. Их можно идентифицировать по записи FileSystem в столбце "Поставщик". (Диски файловой системы в Windows PowerShell поддерживаются поставщиком FileSystem Windows PowerShell.)

Чтобы просмотреть синтаксис командлета **Get-PSDrive**, введите команду **Get-Command** с параметром **Syntax**.

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

Параметр **PSProvider** позволит отобразить только диски Windows PowerShell, поддерживаемые конкретным поставщиком. Например, чтобы отобразить только те диски Windows PowerShell, которые поддерживаются поставщиком FileSystem Windows PowerShell, введите команду **Get-PSDrive** с параметром **PSProvider** и значением **FileSystem**.

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

Чтобы просмотреть диски Windows PowerShell, представляющие кусты реестра, используйте параметр **PSProvider** для отображения только тех дисков Windows PowerShell, которые поддерживаются поставщиком реестра Windows PowerShell:

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

С дисками Windows PowerShell также можно использовать стандартные командлеты расположения:

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

## <a name="adding-new-windows-powershell-drives-new-psdrive"></a>Добавление новых дисков Windows PowerShell (New-PSDrive)

Добавить собственные диски Windows PowerShell можно с помощью команды **New-PSDrive**. Чтобы получить синтаксис для команды **New-PSDrive**, введите команду **Get-Command** с параметром **Syntax**.

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

Чтобы создать новый диск Windows PowerShell, необходимо указать три параметра:

- имя диска (можно использовать любое допустимое имя Windows PowerShell);

- PSProvider (используйте FileSystem для расположений файловой системы и Registry для расположений реестра);

- корень, т. е. путь к корню нового диска.

Например, можно создать диск с именем "Office", который сопоставляется с папкой, содержащей приложения Microsoft Office на компьютере, такой как **C:\\Program Files\\Microsoft Office\\OFFICE11**. Чтобы создать диск, введите следующую команду:

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Microsoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> Обычно пути не зависят от регистра.

Ссылка на новый диск Windows PowerShell, как и на все диски Windows PowerShell, указывается по его имени, за которым следует двоеточие ( **:** ).

Диск Windows PowerShell может упростить множество задач. Например, некоторые наиболее важные разделы в реестре Windows содержат слишком длинные пути, что делает их громоздкими и сложными для запоминания. Критически важные сведения о конфигурации находятся в разделе **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**. Чтобы просмотреть и изменить элементы в разделе реестра CurrentVersion, можно создать диск Windows PowerShell, корень которого находится в этом разделе, введя:

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\Windows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

После этого можно изменить расположение на диск **cvkey:** (как и для любого другого диска):

```
PS> cd cvkey:
```

или:

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

Командлет New-PsDrive добавляет новый диск только в текущий сеанс Windows PowerShell. Если закрыть окно Windows PowerShell, новый диск будет потерян. Чтобы сохранить диск Windows PowerShell, используйте командлет Export-Console для экспорта текущего сеанса Windows PowerShell, а затем используйте параметр **PSConsoleFile** PowerShell.exe для импорта. Также можно добавить новый диск в профиль Windows PowerShell.

## <a name="deleting-windows-powershell-drives-remove-psdrive"></a>Удаление дисков Windows PowerShell (Remove-PSDrive)

Диски из Windows PowerShell можно удалить, используя командлет **Remove-PSDrive**. Командлет **Remove-PSDrive** прост в использовании. Чтобы удалить определенный диск Windows PowerShell, необходимо только указать имя диска Windows PowerShell.

Например, если вы добавили диск Windows PowerShell **Office:** , как описано в разделе **New-PSDrive**, вы можете удалить его, выполнив следующую команду:

```powershell
Remove-PSDrive -Name Office
```

Чтобы удалить диск Windows PowerShell **cvkey:** , описанный в предыдущем разделе **New-PSDrive**, выполните следующую команду:

```powershell
Remove-PSDrive -Name cvkey
```

Удалить диск Windows PowerShell легко, но его невозможно удалить, если он открыт. Например:

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

## <a name="adding-and-removing-drives-outside-windows-powershell"></a>Добавление и удаление дисков за пределами Windows PowerShell

Windows PowerShell обнаруживает диски файловой системы, которые добавляются или удаляются в Windows, включая сопоставленные сетевые диски, подключенные USB-накопители и удаленные диски, с помощью команды **net use** или методов **WScript.Network MapNetworkDrive** и **RemoveNetworkDrive** сценария сервера сценариев Windows (WSH).
