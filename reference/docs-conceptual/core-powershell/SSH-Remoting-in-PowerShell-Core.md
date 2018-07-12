
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="b5da0-101">Удаленное взаимодействие с PowerShell через SSH</span><span class="sxs-lookup"><span data-stu-id="b5da0-101">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="b5da0-102">Обзор</span><span class="sxs-lookup"><span data-stu-id="b5da0-102">Overview</span></span>

<span data-ttu-id="b5da0-103">Функция удаленного взаимодействия PowerShell обычно использует WinRM для согласования соединения и передачи данных.</span><span class="sxs-lookup"><span data-stu-id="b5da0-103">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span>
<span data-ttu-id="b5da0-104">Протокол SSH был выбран для этой реализации удаленного взаимодействия, так как он теперь доступен для платформ Linux и Windows и позволяет реализовать действительно многоплатформенное удаленное взаимодействие PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5da0-104">SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>
<span data-ttu-id="b5da0-105">Однако WinRM также предоставляет надежную модель размещения для удаленных сеансов PowerShell, которой пока нет в этой реализации.</span><span class="sxs-lookup"><span data-stu-id="b5da0-105">However, WinRM also provides a robust hosting model for PowerShell remote sessions which this implementation does not yet do.</span></span>
<span data-ttu-id="b5da0-106">Это значит, что конфигурация удаленной конечной точки PowerShell и JEA (Just Enough Administration) в этой реализации пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b5da0-106">And this means that PowerShell remote endpoint configuration and JEA (Just Enough Administration) is not yet supported in this implementation.</span></span>

<span data-ttu-id="b5da0-107">Удаленное взаимодействие по SSH в PowerShell позволяет выполнять базовые операции удаленной работы с сеансами PowerShell между компьютерами с Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="b5da0-107">PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span>
<span data-ttu-id="b5da0-108">Для этого на целевом компьютере создается ведущий процесс PowerShell в качестве подсистемы SSH.</span><span class="sxs-lookup"><span data-stu-id="b5da0-108">This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="b5da0-109">В конечном счете, все это будет заменено более общей моделью размещения, которая аналогична тому, как WinRM обеспечивает поддержку конфигурации конечной точки и JEA.</span><span class="sxs-lookup"><span data-stu-id="b5da0-109">Eventually this will be changed to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="b5da0-110">Командлеты `New-PSSession`, `Enter-PSSession` и `Invoke-Command` теперь имеют новый набор параметров, призванный упростить новое удаленное подключение.</span><span class="sxs-lookup"><span data-stu-id="b5da0-110">The `New-PSSession`, `Enter-PSSession` and `Invoke-Command` cmdlets now have a new parameter set to facilitate this new remoting connection</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="b5da0-111">Этот новый набор параметров, скорее всего, изменится, но сейчас он позволяет создавать сеансы SSH PSSession, с которыми можно взаимодействовать с помощью командной строки либо вызова команд и сценариев.</span><span class="sxs-lookup"><span data-stu-id="b5da0-111">This new parameter set will likely change but for now allows you to create SSH PSSessions that you can interact with from the command line or invoke commands and scripts on.</span></span>
<span data-ttu-id="b5da0-112">Вы можете указать целевой компьютер с помощью параметра HostName и имя пользователя с помощью параметра UserName.</span><span class="sxs-lookup"><span data-stu-id="b5da0-112">You specify the target machine with the HostName parameter and provide the user name with UserName.</span></span>
<span data-ttu-id="b5da0-113">При интерактивном выполнении командлетов в командной строке PowerShell вам будет предложено ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="b5da0-113">When running the cmdlets interactively at the PowerShell command line you will be prompted for a password.</span></span>
<span data-ttu-id="b5da0-114">Но вы также можете использовать проверку подлинности на основе ключа SSH и указать путь к файлу закрытого ключа с помощью параметра KeyFilePath.</span><span class="sxs-lookup"><span data-stu-id="b5da0-114">But you also have the option to use SSH key authentication and provide a private key file path with the KeyFilePath parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="b5da0-115">Общие сведения об установке</span><span class="sxs-lookup"><span data-stu-id="b5da0-115">General setup information</span></span>

<span data-ttu-id="b5da0-116">SSH должен быть установлен на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="b5da0-116">SSH is required to be installed on all machines.</span></span>
<span data-ttu-id="b5da0-117">Вам нужно установить клиент (`ssh.exe`) и сервер (`sshd.exe`), чтобы можно было поэкспериментировать с удаленным взаимодействием к компьютерам и с них.</span><span class="sxs-lookup"><span data-stu-id="b5da0-117">You should install both client (`ssh.exe`) and server (`sshd.exe`) so that you can experiment with remoting to and from the machines.</span></span>
<span data-ttu-id="b5da0-118">Для Windows нужно установить [Win32 OpenSSH из GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="b5da0-118">For Windows you will need to install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="b5da0-119">Для Linux нужно установить SSH (включая сервер sshd) в соответствии с используемой платформой.</span><span class="sxs-lookup"><span data-stu-id="b5da0-119">For Linux you will need to install SSH (including sshd server) appropriate to your platform.</span></span>
<span data-ttu-id="b5da0-120">Вам также потребуется новая версия сборки или пакета PowerShell с GitHub, где есть функция удаленного взаимодействия SSH.</span><span class="sxs-lookup"><span data-stu-id="b5da0-120">You will also need a recent PowerShell build or package from GitHub having the SSH remoting feature.</span></span>
<span data-ttu-id="b5da0-121">Подсистемы SSH используются для запуска процесса PowerShell на удаленном компьютере, поэтому сервер SSH нужно настроить соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b5da0-121">SSH subsystems is used to establish a PowerShell process on the remote machine and the SSH server will need to be configured for that.</span></span>
<span data-ttu-id="b5da0-122">Кроме того, нужно включить проверку подлинности с помощью пароля и при необходимости проверку подлинности на основе ключа.</span><span class="sxs-lookup"><span data-stu-id="b5da0-122">In addition you will need to enable password authentication and optionally key based authentication.</span></span>

## <a name="setup-on-windows-machine"></a><span data-ttu-id="b5da0-123">Установка на компьютере с Windows</span><span class="sxs-lookup"><span data-stu-id="b5da0-123">Setup on Windows Machine</span></span>

1. <span data-ttu-id="b5da0-124">Установите последнюю версию [PowerShell Core для Windows].</span><span class="sxs-lookup"><span data-stu-id="b5da0-124">Install the latest version of [PowerShell Core for Windows]</span></span>
   - <span data-ttu-id="b5da0-125">Чтобы узнать о наличии поддержки удаленного взаимодействия SSH, просмотрите набор параметров для `New-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="b5da0-125">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="b5da0-126">Установите последнюю версию сборки [Win32 OpenSSH] из GitHub, используя [инструкции по установке].</span><span class="sxs-lookup"><span data-stu-id="b5da0-126">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
3. <span data-ttu-id="b5da0-127">Измените файл sshd_config в том расположении, куда вы установили Win32 OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="b5da0-127">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>
   - <span data-ttu-id="b5da0-128">Включите проверку подлинности с помощью пароля:</span><span class="sxs-lookup"><span data-stu-id="b5da0-128">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

    ```
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```

    > [!NOTE]
    <span data-ttu-id="b5da0-129">В OpenSSH для Windows обнаружена ошибка, блокирующая работу пробелов в путях к исполняемым файлам подсистемы.</span><span class="sxs-lookup"><span data-stu-id="b5da0-129">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span>
    <span data-ttu-id="b5da0-130">Дополнительные сведения об [этой проблеме см. на сайте GitHub](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="b5da0-130">See [this issue on GitHub for more information](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

    <span data-ttu-id="b5da0-131">Одно из решений — создать символьную ссылку на каталог установки Powershell, которая не содержит пробелы:</span><span class="sxs-lookup"><span data-stu-id="b5da0-131">One solution is to create a symlink to the Powershell installation directory that does not contain spaces:</span></span>

    ```powershell
    mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
    ```

    <span data-ttu-id="b5da0-132">а затем ввести ее в подсистеме:</span><span class="sxs-lookup"><span data-stu-id="b5da0-132">and then enter it in the subsystem:</span></span>

    ```
    Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
    ```

   ```
   Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="b5da0-133">При необходимости включите проверку подлинности на основе ключа:</span><span class="sxs-lookup"><span data-stu-id="b5da0-133">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="b5da0-134">Перезапустите службу sshd.</span><span class="sxs-lookup"><span data-stu-id="b5da0-134">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="b5da0-135">Добавьте путь установки OpenSSH в свою переменную пути Env.</span><span class="sxs-lookup"><span data-stu-id="b5da0-135">Add the path where OpenSSH is installed to your Path Env Variable</span></span>
   - <span data-ttu-id="b5da0-136">Это нужно сделать в соответствии с `C:\Program Files\OpenSSH\`.</span><span class="sxs-lookup"><span data-stu-id="b5da0-136">This should be along the lines of `C:\Program Files\OpenSSH\`</span></span>
   - <span data-ttu-id="b5da0-137">Это позволяет найти ssh.exe.</span><span class="sxs-lookup"><span data-stu-id="b5da0-137">This allows for the ssh.exe to be found</span></span>

## <a name="setup-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="b5da0-138">Установка на компьютере с Linux (Ubuntu 14.04)</span><span class="sxs-lookup"><span data-stu-id="b5da0-138">Setup on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="b5da0-139">Установите последнюю сборку [PowerShell Core для Linux] из GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5da0-139">Install the latest [PowerShell Core for Linux] build from GitHub</span></span>
2. <span data-ttu-id="b5da0-140">При необходимости установите [Ubuntu SSH].</span><span class="sxs-lookup"><span data-stu-id="b5da0-140">Install [Ubuntu SSH] as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="b5da0-141">Измените файл sshd_config в расположении /etc/ssh.</span><span class="sxs-lookup"><span data-stu-id="b5da0-141">Edit the sshd_config file at location /etc/ssh</span></span>
   - <span data-ttu-id="b5da0-142">Включите проверку подлинности с помощью пароля:</span><span class="sxs-lookup"><span data-stu-id="b5da0-142">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="b5da0-143">Добавьте запись подсистемы PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b5da0-143">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="b5da0-144">При необходимости включите проверку подлинности на основе ключа:</span><span class="sxs-lookup"><span data-stu-id="b5da0-144">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="b5da0-145">Перезапустите службу sshd.</span><span class="sxs-lookup"><span data-stu-id="b5da0-145">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="setup-on-macos-machine"></a><span data-ttu-id="b5da0-146">Установка на компьютере с MacOS</span><span class="sxs-lookup"><span data-stu-id="b5da0-146">Setup on MacOS Machine</span></span>

1. <span data-ttu-id="b5da0-147">Установите последнюю сборку [PowerShell Core для MacOS].</span><span class="sxs-lookup"><span data-stu-id="b5da0-147">Install the latest [PowerShell Core for MacOS] build</span></span>
   - <span data-ttu-id="b5da0-148">Убедитесь, что удаленное взаимодействие SSH включено, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b5da0-148">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="b5da0-149">Откройте `System Preferences`.</span><span class="sxs-lookup"><span data-stu-id="b5da0-149">Open `System Preferences`</span></span>
     - <span data-ttu-id="b5da0-150">Щелкните `Sharing`.</span><span class="sxs-lookup"><span data-stu-id="b5da0-150">Click on `Sharing`</span></span>
     - <span data-ttu-id="b5da0-151">Убедитесь, что `Remote Login` имеет значение `Remote Login: On`.</span><span class="sxs-lookup"><span data-stu-id="b5da0-151">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="b5da0-152">Разрешите доступ соответствующим пользователям.</span><span class="sxs-lookup"><span data-stu-id="b5da0-152">Allow access to appropriate users</span></span>
2. <span data-ttu-id="b5da0-153">Измените файл `sshd_config` в расположении `/private/etc/ssh/sshd_config`.</span><span class="sxs-lookup"><span data-stu-id="b5da0-153">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>
   - <span data-ttu-id="b5da0-154">Используйте привычный вам редактор или следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5da0-154">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="b5da0-155">Включите проверку подлинности с помощью пароля:</span><span class="sxs-lookup"><span data-stu-id="b5da0-155">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="b5da0-156">Добавьте запись подсистемы PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b5da0-156">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="b5da0-157">При необходимости включите проверку подлинности на основе ключа:</span><span class="sxs-lookup"><span data-stu-id="b5da0-157">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="b5da0-158">Перезапустите службу sshd.</span><span class="sxs-lookup"><span data-stu-id="b5da0-158">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="powershell-remoting-example"></a><span data-ttu-id="b5da0-159">Пример удаленного взаимодействия PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5da0-159">PowerShell Remoting Example</span></span>

<span data-ttu-id="b5da0-160">Проще всего проверить удаленное взаимодействие, просто попробовав использовать его на отдельном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b5da0-160">The easiest way to test remoting is to just try it on a single machine.</span></span>
<span data-ttu-id="b5da0-161">Здесь я создам удаленный сеанс на том же компьютере в окне Linux.</span><span class="sxs-lookup"><span data-stu-id="b5da0-161">Here I will create a remote session back to the same machine on a Linux box.</span></span>
<span data-ttu-id="b5da0-162">Обратите внимание, что я использую командлеты PowerShell из командной строки, поэтому мы видим запросы SSH о проверке главного компьютера, а также запросы на ввод пароля.</span><span class="sxs-lookup"><span data-stu-id="b5da0-162">Notice that I am using PowerShell cmdlets from a command prompt so we see prompts from SSH asking to verify the host computer as well as password prompts.</span></span>
<span data-ttu-id="b5da0-163">То же самое можно сделать на компьютере с Windows, чтобы убедиться в работе удаленного взаимодействия, а затем удаленно переключаться между компьютерами, просто изменяя имя узла.</span><span class="sxs-lookup"><span data-stu-id="b5da0-163">You can do the same thing on a Windows machine to ensure remoting is working there and then remote between machines by simply changing the host name.</span></span>

```powershell
#
# Linux to Linux
#
$session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
```

```output
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:
```

```powershell
$session
```

```output
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            UbuntuVM1       RemoteMachine   Opened        DefaultShell             Available
```

```powershell
Enter-PSSession $session
```

```output
[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession
```

```powershell
Invoke-Command $session -ScriptBlock { Get-Process powershell }
```

```output
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1
```

```powershell
#
# Linux to Windows
#
Enter-PSSession -HostName WinVM1 -UserName PTestName
```

```output
PTestName@WinVM1s password:
```

```powershell
[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver
```

```output
Microsoft Windows [Version 10.0.10586]
```

```powershell
#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
```

```output
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.
```

```powershell
$session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
```

```output
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
```

```powershell
$session
```

```output
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available
```

```powershell
Enter-PSSession -Session $session
```

```output
[WinVM2]: PS C:\Users\PSRemoteUser\Documents> $PSVersionTable

Name                           Value
----                           -----
PSEdition                      Core
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
SerializationVersion           1.1.0.1
BuildVersion                   3.0.0.0
CLRVersion
PSVersion                      6.0.0-alpha
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
GitCommitId                    v6.0.0-alpha.17


[WinVM2]: PS C:\Users\PSRemoteUser\Documents>
```

### <a name="known-issues"></a><span data-ttu-id="b5da0-164">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="b5da0-164">Known Issues</span></span>

- <span data-ttu-id="b5da0-165">Команда sudo не работает во входящем удаленном сеансе на компьютер Linux.</span><span class="sxs-lookup"><span data-stu-id="b5da0-165">sudo command does not work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="b5da0-166">См. также</span><span class="sxs-lookup"><span data-stu-id="b5da0-166">See Also</span></span>

[<span data-ttu-id="b5da0-167">PowerShell Core для Windows</span><span class="sxs-lookup"><span data-stu-id="b5da0-167">PowerShell Core for Windows</span></span>](../setup/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="b5da0-168">PowerShell Core для Windows</span><span class="sxs-lookup"><span data-stu-id="b5da0-168">PowerShell Core for Linux</span></span>](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="b5da0-169">PowerShell Core для MacOS</span><span class="sxs-lookup"><span data-stu-id="b5da0-169">PowerShell Core for MacOS</span></span>](../setup/installing-powershell-core-on-macos.md)

[<span data-ttu-id="b5da0-170">Win32 OpenSSH</span><span class="sxs-lookup"><span data-stu-id="b5da0-170">Win32 OpenSSH</span></span>](https://github.com/PowerShell/Win32-OpenSSH/releases)

[<span data-ttu-id="b5da0-171">установка</span><span class="sxs-lookup"><span data-stu-id="b5da0-171">installation</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[<span data-ttu-id="b5da0-172">Ubuntu SSH</span><span class="sxs-lookup"><span data-stu-id="b5da0-172">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)