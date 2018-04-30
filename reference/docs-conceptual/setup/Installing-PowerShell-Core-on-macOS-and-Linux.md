# <a name="installing-powershell-core-on-macos-and-linux"></a><span data-ttu-id="72eb7-101">Установка PowerShell Core в macOS и Linux</span><span class="sxs-lookup"><span data-stu-id="72eb7-101">Installing PowerShell Core on macOS and Linux</span></span>

<span data-ttu-id="72eb7-102">Поддерживает [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], [Arch Linux][arch] и [macOS 10.12][mac].</span><span class="sxs-lookup"><span data-stu-id="72eb7-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], [Arch Linux][arch], and [macOS 10.12][mac].</span></span>

<span data-ttu-id="72eb7-103">Для дистрибутивов Linux без официальной поддержки попробуйте использовать [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="72eb7-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span> <span data-ttu-id="72eb7-104">Можно также попытаться развернуть двоичные файлы PowerShell напрямую с помощью [архива`tar.gz`][tar] Linux, но при этом нужно отдельно настроить необходимые зависимости с учетом операционной системы.</span><span class="sxs-lookup"><span data-stu-id="72eb7-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="72eb7-105">Все пакеты доступны на нашей странице [выпусков][] GitHub.</span><span class="sxs-lookup"><span data-stu-id="72eb7-105">All packages are available on our GitHub [releases][] page.</span></span> <span data-ttu-id="72eb7-106">После установки пакета запустите `pwsh` из терминала.</span><span class="sxs-lookup"><span data-stu-id="72eb7-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1704
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fed25]: #fedora-25
[fed26]: #fedora-26
[arch]: #arch-linux
[lai]: #linux-appimage
[mac]: #macos-1012
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="72eb7-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="72eb7-108">Установка с помощью репозитория пакетов — Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="72eb7-109">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="72eb7-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span> <span data-ttu-id="72eb7-110">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="72eb7-110">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-111">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="72eb7-111">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="72eb7-112">Установка с помощью прямого скачивания — Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-112">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="72eb7-113">Скачайте пакет Debian `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="72eb7-113">Download the Debian package `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.14.04_amd64.deb
```

<span data-ttu-id="72eb7-114">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-114">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="72eb7-115">Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-115">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="72eb7-116">Удаление — Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-116">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="72eb7-117">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-117">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="72eb7-118">Установка с помощью репозитория пакетов — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-118">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="72eb7-119">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="72eb7-119">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="72eb7-120">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="72eb7-120">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-121">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="72eb7-121">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="72eb7-122">Установка с помощью прямого скачивания — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-122">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="72eb7-123">Скачайте пакет Debian `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="72eb7-123">Download the Debian package `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
```

<span data-ttu-id="72eb7-124">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-124">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="72eb7-125">Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-125">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="72eb7-126">Удаление — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-126">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="72eb7-127">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-127">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="72eb7-128">Установка с помощью репозитория пакетов — Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-128">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="72eb7-129">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="72eb7-129">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="72eb7-130">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="72eb7-130">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/17.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-131">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="72eb7-131">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="72eb7-132">Установка с помощью прямого скачивания — Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-132">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="72eb7-133">Скачайте пакет Debian `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="72eb7-133">Download the Debian package `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.17.04_amd64.deb
```

<span data-ttu-id="72eb7-134">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-134">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="72eb7-135">Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-135">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="72eb7-136">Удаление — Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-136">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="72eb7-137">Debian 8</span><span class="sxs-lookup"><span data-stu-id="72eb7-137">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="72eb7-138">Установка с помощью репозитория пакетов — Debian 8</span><span class="sxs-lookup"><span data-stu-id="72eb7-138">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="72eb7-139">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="72eb7-139">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="72eb7-140">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="72eb7-140">This is the preferred method.</span></span>

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-141">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="72eb7-141">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="72eb7-142">Установка с помощью прямого скачивания — Debian 8</span><span class="sxs-lookup"><span data-stu-id="72eb7-142">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="72eb7-143">Скачайте пакет Debian `powershell_6.0.0-1.debian.8_amd64.deb` со страницы [выпусков][] на компьютер с Debian:</span><span class="sxs-lookup"><span data-stu-id="72eb7-143">Download the Debian package `powershell_6.0.0-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.8_amd64.deb
```

<span data-ttu-id="72eb7-144">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-144">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="72eb7-145">Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-145">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="72eb7-146">Удаление — Debian 8</span><span class="sxs-lookup"><span data-stu-id="72eb7-146">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="72eb7-147">Debian 9</span><span class="sxs-lookup"><span data-stu-id="72eb7-147">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="72eb7-148">Установка с помощью репозитория пакетов — Debian 9</span><span class="sxs-lookup"><span data-stu-id="72eb7-148">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="72eb7-149">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="72eb7-149">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="72eb7-150">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="72eb7-150">This is the preferred method.</span></span>

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl gnupg apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-151">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="72eb7-151">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="72eb7-152">Установка с помощью прямого скачивания — Debian 9</span><span class="sxs-lookup"><span data-stu-id="72eb7-152">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="72eb7-153">Скачайте пакет Debian `powershell_6.0.0-1.debian.9_amd64.deb` со страницы [выпусков][] на компьютер с Debian:</span><span class="sxs-lookup"><span data-stu-id="72eb7-153">Download the Debian package `powershell_6.0.0-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

<span data-ttu-id="72eb7-154">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-154">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="72eb7-155">Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-155">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="72eb7-156">Удаление — Debian 9</span><span class="sxs-lookup"><span data-stu-id="72eb7-156">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="72eb7-157">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-157">CentOS 7</span></span>

> <span data-ttu-id="72eb7-158">Этот пакет также работает в Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="72eb7-158">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="72eb7-159">Установка с помощью репозитория пакетов (рекомендуется) — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-159">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="72eb7-160">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="72eb7-160">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-161">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo yum update powershell` для обновления PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-161">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="72eb7-162">Установка с помощью прямого скачивания — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-162">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="72eb7-163">Используя [CentOS 7][], скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с CentOS:</span><span class="sxs-lookup"><span data-stu-id="72eb7-163">Using [CentOS 7][], download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-164">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-164">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-165">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="72eb7-165">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="72eb7-166">Удаление — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-166">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="72eb7-168">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-168">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="72eb7-169">Установка с помощью репозитория пакетов (рекомендуется) — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-169">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="72eb7-170">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="72eb7-170">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="72eb7-171">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo yum update powershell` для обновления PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-171">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="72eb7-172">Установка с помощью прямого скачивания — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-172">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="72eb7-173">Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Red Hat Enterprise Linux:</span><span class="sxs-lookup"><span data-stu-id="72eb7-173">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

<span data-ttu-id="72eb7-174">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-174">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-175">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="72eb7-175">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="72eb7-176">Удаление — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-176">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="72eb7-177">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="72eb7-177">OpenSUSE 42.2</span></span>

> <span data-ttu-id="72eb7-178">**Примечание**. При установке PowerShell Core `zypper` может вывести следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="72eb7-178">**Note:** When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```text
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="72eb7-179">В этом случае убедитесь в наличии совместимой библиотеки `libcurl`, проверив, что в результате выполнения следующей команды пакет `libcurl4` отображается как установленный:</span><span class="sxs-lookup"><span data-stu-id="72eb7-179">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="72eb7-180">Затем при установке пакета `powershell` выберите решение `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-180">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the `powershell` package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="72eb7-181">Установка с помощью репозитория пакетов (рекомендуется) — OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="72eb7-181">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="72eb7-182">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="72eb7-182">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Product feed
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/zypp/repos.d/microsoft.repo

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="72eb7-183">Установка с помощью прямого скачивания — OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="72eb7-183">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="72eb7-184">Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с OpenSUSE:</span><span class="sxs-lookup"><span data-stu-id="72eb7-184">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-185">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="72eb7-185">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="72eb7-186">Удаление — OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="72eb7-186">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a><span data-ttu-id="72eb7-187">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="72eb7-187">Fedora 25</span></span>

### <a name="installation-via-package-repository-preferred---fedora-25"></a><span data-ttu-id="72eb7-188">Установка с помощью репозитория пакетов (рекомендуется) — Fedora 25</span><span class="sxs-lookup"><span data-stu-id="72eb7-188">Installation via Package Repository (preferred) - Fedora 25</span></span>

<span data-ttu-id="72eb7-189">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="72eb7-189">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-25"></a><span data-ttu-id="72eb7-190">Установка с помощью прямого скачивания — Fedora 25</span><span class="sxs-lookup"><span data-stu-id="72eb7-190">Installation via Direct Download - Fedora 25</span></span>

<span data-ttu-id="72eb7-191">Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Fedora:</span><span class="sxs-lookup"><span data-stu-id="72eb7-191">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-192">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-192">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-193">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="72eb7-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a><span data-ttu-id="72eb7-194">Удаление — Fedora 25</span><span class="sxs-lookup"><span data-stu-id="72eb7-194">Uninstallation - Fedora 25</span></span>

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a><span data-ttu-id="72eb7-195">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="72eb7-195">Fedora 26</span></span>

### <a name="installation-via-package-repository-preferred---fedora-26"></a><span data-ttu-id="72eb7-196">Установка с помощью репозитория пакетов (рекомендуется) — Fedora 26</span><span class="sxs-lookup"><span data-stu-id="72eb7-196">Installation via Package Repository (preferred) - Fedora 26</span></span>

<span data-ttu-id="72eb7-197">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="72eb7-197">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install a system component
sudo dnf install compat-openssl10

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-26"></a><span data-ttu-id="72eb7-198">Установка с помощью прямого скачивания — Fedora 26</span><span class="sxs-lookup"><span data-stu-id="72eb7-198">Installation via Direct Download - Fedora 26</span></span>

<span data-ttu-id="72eb7-199">Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Fedora:</span><span class="sxs-lookup"><span data-stu-id="72eb7-199">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-200">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-200">Then execute the following in the terminal:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="72eb7-201">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="72eb7-201">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a><span data-ttu-id="72eb7-202">Удаление — Fedora 26</span><span class="sxs-lookup"><span data-stu-id="72eb7-202">Uninstallation - Fedora 26</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="72eb7-203">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="72eb7-203">Arch Linux</span></span>

<span data-ttu-id="72eb7-204">PowerShell можно получить из пользовательского репозитория [Arch Linux][] (AUR).</span><span class="sxs-lookup"><span data-stu-id="72eb7-204">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="72eb7-205">Его можно скомпилировать с помощью [последнего выпуска с тегами][arch-release].</span><span class="sxs-lookup"><span data-stu-id="72eb7-205">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="72eb7-206">Его можно скомпилировать из [последней фиксации в основной репозиторий][arch-git].</span><span class="sxs-lookup"><span data-stu-id="72eb7-206">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="72eb7-207">Его можно установить с помощью [двоичного файла последнего выпуска][arch-bin].</span><span class="sxs-lookup"><span data-stu-id="72eb7-207">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="72eb7-208">Пакеты в AUR обслуживаются сообществом — официальная поддержка отсутствует.</span><span class="sxs-lookup"><span data-stu-id="72eb7-208">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="72eb7-209">Дополнительные сведения об установке пакетов из AUR см. на [вики-сайте Arch Linux](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) или в [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile) сообщества.</span><span class="sxs-lookup"><span data-stu-id="72eb7-209">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="72eb7-211">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="72eb7-211">Linux AppImage</span></span>

<span data-ttu-id="72eb7-212">Используя последний дистрибутив Linux, скачайте AppImage `powershell-6.0.0-x86_64.AppImage` со страницы [выпусков][] на компьютер с Linux.</span><span class="sxs-lookup"><span data-stu-id="72eb7-212">Using a recent Linux distribution, download the AppImage `powershell-6.0.0-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="72eb7-213">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="72eb7-213">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.0-x86_64.AppImage
./powershell-6.0.0-x86_64.AppImage
```

<span data-ttu-id="72eb7-214">[AppImage][] позволяет запустить PowerShell, не устанавливая его.</span><span class="sxs-lookup"><span data-stu-id="72eb7-214">The [AppImage][] lets you run PowerShell without installing it.</span></span> <span data-ttu-id="72eb7-215">Это переносимое приложение, которое объединяет PowerShell и его зависимости (включая системные зависимости .NET Core) в единый пакет.</span><span class="sxs-lookup"><span data-stu-id="72eb7-215">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span> <span data-ttu-id="72eb7-216">Этот пакет работает независимо от дистрибутива Linux пользователя и представляет собой отдельный двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="72eb7-216">This package works independently of the user's Linux distribution, and is a single binary.</span></span>

[appimage]: http://appimage.org/

## <a name="macos-1012"></a><span data-ttu-id="72eb7-218">macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="72eb7-218">macOS 10.12</span></span>

### <a name="installation-via-homebrew-preferred---macos-1012"></a><span data-ttu-id="72eb7-219">Установка с помощью Homebrew (рекомендуется) — macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="72eb7-219">Installation via Homebrew (preferred) - macOS 10.12</span></span>

<span data-ttu-id="72eb7-220">[Homebrew][brew] — это диспетчер отсутствующих пакетов для macOS.</span><span class="sxs-lookup"><span data-stu-id="72eb7-220">[Homebrew][brew] is the missing package manager for macOS.</span></span> <span data-ttu-id="72eb7-221">Если команда `brew` не найдена, нужно установить Homebrew по [соответствующим инструкциям][brew].</span><span class="sxs-lookup"><span data-stu-id="72eb7-221">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="72eb7-222">После установки Homebrew установка PowerShell не вызывает проблем.</span><span class="sxs-lookup"><span data-stu-id="72eb7-222">Once you've installed Homebrew, installing PowerShell is easy.</span></span> <span data-ttu-id="72eb7-223">Сначала установите [Homebrew-Cask][cask], чтобы можно было установить дополнительные пакеты:</span><span class="sxs-lookup"><span data-stu-id="72eb7-223">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="72eb7-224">Теперь можно установить PowerShell:</span><span class="sxs-lookup"><span data-stu-id="72eb7-224">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="72eb7-225">После выпуска новых версий PowerShell просто обновите формулы Homebrew и PowerShell:</span><span class="sxs-lookup"><span data-stu-id="72eb7-225">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> <span data-ttu-id="72eb7-226">Примечание. Приведенные выше команды можно вызвать из узла PowerShell (pwsh), но затем потребуется выйти из оболочки PowerShell и повторно войти в нее, чтобы завершить обновление и обновить значения в таблице $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="72eb7-226">Note: The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and re-entered to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download---macos-1012"></a><span data-ttu-id="72eb7-227">Установка с помощью прямого скачивания — macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="72eb7-227">Installation via Direct Download - macOS 10.12</span></span>

<span data-ttu-id="72eb7-228">Используя macOS 10.12, скачайте пакет PKG `powershell-6.0.0-osx.10.12-x64.pkg` со страницы [выпусков][] на компьютер с macOS.</span><span class="sxs-lookup"><span data-stu-id="72eb7-228">Using macOS 10.12, download the PKG package `powershell-6.0.0-osx.10.12-x64.pkg` from the [releases][] page onto the macOS machine.</span></span>

<span data-ttu-id="72eb7-229">Дважды щелкните файл и следуйте инструкциям на экране либо установите его из терминала:</span><span class="sxs-lookup"><span data-stu-id="72eb7-229">Either double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.0-osx.10.12-x64.pkg -target /
```

### <a name="uninstallation---macos-1012"></a><span data-ttu-id="72eb7-230">Удаление — macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="72eb7-230">Uninstallation - macOS 10.12</span></span>

<span data-ttu-id="72eb7-231">Если вы установили PowerShell с помощью Homebrew, удаление осуществляется очень просто:</span><span class="sxs-lookup"><span data-stu-id="72eb7-231">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="72eb7-232">Если вы установили PowerShell с помощью прямого скачивания, PowerShell нужно удалить вручную:</span><span class="sxs-lookup"><span data-stu-id="72eb7-232">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="72eb7-233">Чтобы удалить дополнительные пути PowerShell (например, путь к профилю пользователя), см. раздел [Пути][paths] ниже и удалите требуемые пути с помощью `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-233">To uninstall the additional PowerShell paths (such as the user profile path) please see the [paths][paths] section below in this document and remove the desired the paths with `sudo rm`.</span></span> <span data-ttu-id="72eb7-234">(Примечание. Это не требуется в случае установки с помощью Homebrew.)</span><span class="sxs-lookup"><span data-stu-id="72eb7-234">(Note: this is not necessary if you installed with Homebrew.)</span></span>

[paths]:#paths

## <a name="kali"></a><span data-ttu-id="72eb7-235">Kali</span><span class="sxs-lookup"><span data-stu-id="72eb7-235">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="72eb7-236">Установка</span><span class="sxs-lookup"><span data-stu-id="72eb7-236">Installation</span></span>

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Download & Install PowerShell
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="72eb7-237">Запуск PowerShell в последней версии Kali (Kali GNU/Linux Rolling) без его установки</span><span class="sxs-lookup"><span data-stu-id="72eb7-237">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.0-x86_64.AppImage

# Start PowerShell
./powershell-6.0.0-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="72eb7-238">Удаление — Kali</span><span class="sxs-lookup"><span data-stu-id="72eb7-238">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell-6.0.0-x86_64.AppImage
```

## <a name="raspbian"></a><span data-ttu-id="72eb7-239">Raspbian</span><span class="sxs-lookup"><span data-stu-id="72eb7-239">Raspbian</span></span>

<span data-ttu-id="72eb7-240">Сейчас PowerShell поддерживается только в Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="72eb7-240">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

### <a name="installation"></a><span data-ttu-id="72eb7-241">Установка</span><span class="sxs-lookup"><span data-stu-id="72eb7-241">Installation</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="72eb7-242">Удаление — Raspbian</span><span class="sxs-lookup"><span data-stu-id="72eb7-242">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="72eb7-243">Архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="72eb7-243">Binary Archives</span></span>

<span data-ttu-id="72eb7-244">Для поддержки расширенных сценариев развертывания на платформах macOS и Linux доступны архивы двоичных файлов PowerShell `tar.gz`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-244">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="72eb7-245">Зависимости</span><span class="sxs-lookup"><span data-stu-id="72eb7-245">Dependencies</span></span>

<span data-ttu-id="72eb7-246">Для Linux PowerShell создает переносимые двоичные файлы для всех дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="72eb7-246">For Linux, PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="72eb7-247">Однако среда выполнения .NET Core требует различные зависимости для разных дистрибутивов, и поэтому то же самое делает и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72eb7-247">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="72eb7-248">Следующая таблица содержит зависимости .NET Core 2.0 для различных дистрибутивов Linux, которые поддерживаются официально.</span><span class="sxs-lookup"><span data-stu-id="72eb7-248">The following chart shows the .NET Core 2.0 dependencies on different Linux distributions that are officially supported.</span></span>

| <span data-ttu-id="72eb7-249">ОС</span><span class="sxs-lookup"><span data-stu-id="72eb7-249">OS</span></span>                 | <span data-ttu-id="72eb7-250">Зависимости</span><span class="sxs-lookup"><span data-stu-id="72eb7-250">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="72eb7-251">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-251">Ubuntu 14.04</span></span>       | <span data-ttu-id="72eb7-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="72eb7-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="72eb7-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="72eb7-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="72eb7-254">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-254">Ubuntu 16.04</span></span>       | <span data-ttu-id="72eb7-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="72eb7-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="72eb7-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="72eb7-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="72eb7-257">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="72eb7-257">Ubuntu 17.04</span></span>       | <span data-ttu-id="72eb7-258">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="72eb7-258">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="72eb7-259">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="72eb7-259">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="72eb7-260">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="72eb7-260">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="72eb7-261">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="72eb7-261">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="72eb7-262">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="72eb7-262">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="72eb7-263">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="72eb7-263">Debian 9 (Stretch)</span></span> | <span data-ttu-id="72eb7-264">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="72eb7-264">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="72eb7-265">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="72eb7-265">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="72eb7-266">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-266">CentOS 7</span></span> <br> <span data-ttu-id="72eb7-267">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-267">Oracle Linux 7</span></span> <br> <span data-ttu-id="72eb7-268">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="72eb7-268">RHEL 7</span></span> <br> <span data-ttu-id="72eb7-269">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="72eb7-269">OpenSUSE 42.2</span></span> <br> <span data-ttu-id="72eb7-270">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="72eb7-270">Fedora 25</span></span> | <span data-ttu-id="72eb7-271">libunwind, libcurl, openssl-libs, libicu</span><span class="sxs-lookup"><span data-stu-id="72eb7-271">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="72eb7-272">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="72eb7-272">Fedora 26</span></span>          | <span data-ttu-id="72eb7-273">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="72eb7-273">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="72eb7-274">Чтобы развернуть двоичные файлы PowerShell в дистрибутивах Linux без официальной поддержки, вам потребуется отдельно установить необходимые зависимости для целевой ОС.</span><span class="sxs-lookup"><span data-stu-id="72eb7-274">In order to deploy PowerShell binaries on Linux distributions that are not officially supported, you would need to install the necessary dependencies for the target OS in separate steps.</span></span> <span data-ttu-id="72eb7-275">Например, наш [Amazon Linux dockerfile][amazon-dockerfile] сначала устанавливает зависимости, а затем извлекает архив Linux `tar.gz`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-275">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="72eb7-276">Установка — архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="72eb7-276">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="72eb7-277">Linux</span><span class="sxs-lookup"><span data-stu-id="72eb7-277">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.0/pwsh /usr/bin/pwsh
```

#### <a name="macos"></a><span data-ttu-id="72eb7-278">macOS</span><span class="sxs-lookup"><span data-stu-id="72eb7-278">macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.0/pwsh /usr/local/bin/pwsh
```

### <a name="uninstallation---binary-archives"></a><span data-ttu-id="72eb7-279">Удаление — архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="72eb7-279">Uninstallation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="72eb7-280">Linux</span><span class="sxs-lookup"><span data-stu-id="72eb7-280">Linux</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

#### <a name="macos"></a><span data-ttu-id="72eb7-281">macOS</span><span class="sxs-lookup"><span data-stu-id="72eb7-281">macOS</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="72eb7-282">Пути</span><span class="sxs-lookup"><span data-stu-id="72eb7-282">Paths</span></span>

* <span data-ttu-id="72eb7-283">`$PSHOME` имеет значение `/opt/microsoft/powershell/6.0.0/`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-283">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="72eb7-284">Профили пользователей будут считаны из `~/.config/powershell/profile.ps1`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-284">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="72eb7-285">Профили по умолчанию будут считаны из `$PSHOME/profile.ps1`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-285">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="72eb7-286">Модули пользователей будут считаны из `~/.local/share/powershell/Modules`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-286">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="72eb7-287">Общие модули будут считаны из `/usr/local/share/powershell/Modules`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-287">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="72eb7-288">Модули по умолчанию будут считаны из `$PSHOME/Modules`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-288">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="72eb7-289">Журнал PSReadline будет записан в `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-289">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="72eb7-290">Профили учитывают конфигурацию PowerShell для отдельных узлов, поэтому профили конкретных узлов по умолчанию находятся в `Microsoft.PowerShell_profile.ps1` в тех же расположениях.</span><span class="sxs-lookup"><span data-stu-id="72eb7-290">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="72eb7-291">В Linux и macOS учитывается [спецификация базовых каталогов XDG][xdg-bds].</span><span class="sxs-lookup"><span data-stu-id="72eb7-291">On Linux and macOS, the [XDG Base Directory Specification][xdg-bds] is respected.</span></span>

<span data-ttu-id="72eb7-292">Обратите внимание, что, так как macOS является производной от BSD, вместо `/opt` используется префикс `/usr/local`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-292">Note that because macOS is a derivation of BSD, instead of `/opt`, the prefix used is `/usr/local`.</span></span> <span data-ttu-id="72eb7-293">Таким образом, `$PSHOME` имеет значение `/usr/local/microsoft/powershell/6.0.0/`, а символьная ссылка размещается в `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="72eb7-293">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[выпусков]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
