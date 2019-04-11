---
title: Установка PowerShell Core в Linux
description: Сведения об установке PowerShell Core в различных дистрибутивах Linux
ms.date: 08/06/2018
ms.openlocfilehash: 06194550f4e73f9dd38f8cdc25f6c7f698cafce2
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293339"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="c82cf-103">Установка PowerShell Core в Linux</span><span class="sxs-lookup"><span data-stu-id="c82cf-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="c82cf-104">Поддерживается [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora] и [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="c82cf-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810],  [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="c82cf-105">Для дистрибутивов Linux без официальной поддержки попробуйте использовать [snap-пакет PowerShell][snap].</span><span class="sxs-lookup"><span data-stu-id="c82cf-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="c82cf-106">Можно также попытаться развернуть двоичные файлы PowerShell напрямую с помощью [архива`tar.gz`][tar] Linux, но при этом нужно отдельно настроить необходимые зависимости с учетом операционной системы.</span><span class="sxs-lookup"><span data-stu-id="c82cf-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="c82cf-107">Все пакеты доступны на нашей странице [выпусков][] GitHub.</span><span class="sxs-lookup"><span data-stu-id="c82cf-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="c82cf-108">После установки пакета запустите `pwsh` из терминала.</span><span class="sxs-lookup"><span data-stu-id="c82cf-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="c82cf-109">Установка предварительных выпусков</span><span class="sxs-lookup"><span data-stu-id="c82cf-109">Installing Preview Releases</span></span>

<span data-ttu-id="c82cf-110">При установке предварительной версии PowerShell Core для Linux с помощью репозитория пакетов имя пакета меняется с `powershell` на `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="c82cf-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="c82cf-111">При установке с помощью прямого скачивания изменяется только имя файла.</span><span class="sxs-lookup"><span data-stu-id="c82cf-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="c82cf-112">Ниже приведена таблица команд для установки пакетов стабильной и предварительной версий с помощью различных диспетчеров пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="c82cf-113">Дистрибутивы</span><span class="sxs-lookup"><span data-stu-id="c82cf-113">Distribution(s)</span></span>|<span data-ttu-id="c82cf-114">Команда стабильной версии</span><span class="sxs-lookup"><span data-stu-id="c82cf-114">Stable Command</span></span> | <span data-ttu-id="c82cf-115">Команда предварительной версии</span><span class="sxs-lookup"><span data-stu-id="c82cf-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="c82cf-116">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="c82cf-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="c82cf-117">CentOS, RedHat</span><span class="sxs-lookup"><span data-stu-id="c82cf-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="c82cf-118">Fedora</span><span class="sxs-lookup"><span data-stu-id="c82cf-118">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="c82cf-119">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-119">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="c82cf-120">Установка с помощью репозитория пакетов — Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-120">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="c82cf-121">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-121">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c82cf-122">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-122">This is the preferred method.</span></span>

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c82cf-123">В качестве суперпользователя зарегистрируйте репозиторий Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c82cf-123">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="c82cf-124">В дальнейшем для обновления установки необходимо просто использовать `sudo apt-get upgrade powershell`.</span><span class="sxs-lookup"><span data-stu-id="c82cf-124">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="c82cf-125">Установка с помощью прямого скачивания — Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-125">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="c82cf-126">Скачивание пакета Debian</span><span class="sxs-lookup"><span data-stu-id="c82cf-126">Download the Debian package</span></span>
`powershell_6.2.0-1.ubuntu.14.04_amd64.deb`
<span data-ttu-id="c82cf-127">со страницы [выпусков][] на компьютер с Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c82cf-127">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c82cf-128">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-128">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c82cf-129">Команда `dpkg -i` завершается ошибкой при наличии несопоставленных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c82cf-129">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c82cf-130">Следующая команда, `apt-get install -f`, разрешает эти ошибки и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-130">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="c82cf-131">Удаление — Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-131">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="c82cf-132">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-132">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="c82cf-133">Установка с помощью репозитория пакетов — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-133">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="c82cf-134">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-134">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c82cf-135">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-135">This is the preferred method.</span></span>

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c82cf-136">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="c82cf-136">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="c82cf-137">Установка с помощью прямого скачивания — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-137">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="c82cf-138">Скачивание пакета Debian</span><span class="sxs-lookup"><span data-stu-id="c82cf-138">Download the Debian package</span></span>
`powershell_6.2.0-1.ubuntu.16.04_amd64.deb`
<span data-ttu-id="c82cf-139">со страницы [выпусков][] на компьютер с Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c82cf-139">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c82cf-140">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-140">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c82cf-141">Команда `dpkg -i` завершается ошибкой при наличии несопоставленных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c82cf-141">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c82cf-142">Следующая команда, `apt-get install -f`, разрешает эти ошибки и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-142">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="c82cf-143">Удаление — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-143">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="c82cf-144">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-144">Ubuntu 18.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="c82cf-145">Установка с помощью репозитория пакетов — Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-145">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="c82cf-146">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-146">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c82cf-147">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-147">This is the preferred method.</span></span>

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Enable the "universe" repositories
sudo add-apt-repository universe

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c82cf-148">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="c82cf-148">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="c82cf-149">Установка с помощью прямого скачивания — Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-149">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="c82cf-150">Скачивание пакета Debian</span><span class="sxs-lookup"><span data-stu-id="c82cf-150">Download the Debian package</span></span>
`powershell_6.2.0-1.ubuntu.18.04_amd64.deb`
<span data-ttu-id="c82cf-151">со страницы [выпусков][] на компьютер с Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c82cf-151">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c82cf-152">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-152">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c82cf-153">Команда `dpkg -i` завершается ошибкой при наличии несопоставленных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c82cf-153">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c82cf-154">Следующая команда, `apt-get install -f`, разрешает эти ошибки и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-154">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="c82cf-155">Удаление — Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-155">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="c82cf-156">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="c82cf-156">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="c82cf-157">Так как 18.10 — [промежуточная версия](https://www.ubuntu.com/about/release-cycle), она только [поддерживается сообществом](https://docs.microsoft.com/en-us/powershell/scripting/powershell-support-lifecycle?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="c82cf-157">As 18.10 is an [interim release](https://www.ubuntu.com/about/release-cycle), it is only [community supported](https://docs.microsoft.com/en-us/powershell/scripting/powershell-support-lifecycle?view=powershell-6).</span></span>

<span data-ttu-id="c82cf-158">Установка версии 18.10 поддерживается с помощью `snapd`.</span><span class="sxs-lookup"><span data-stu-id="c82cf-158">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="c82cf-159">Полные инструкции см. в разделе [Snap-пакет][snap].</span><span class="sxs-lookup"><span data-stu-id="c82cf-159">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="c82cf-160">Debian 8</span><span class="sxs-lookup"><span data-stu-id="c82cf-160">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="c82cf-161">Установка с помощью репозитория пакетов — Debian 8</span><span class="sxs-lookup"><span data-stu-id="c82cf-161">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="c82cf-162">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-162">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c82cf-163">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-163">This is the preferred method.</span></span>

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

<span data-ttu-id="c82cf-164">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="c82cf-164">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

## <a name="debian-9"></a><span data-ttu-id="c82cf-165">Debian 9</span><span class="sxs-lookup"><span data-stu-id="c82cf-165">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="c82cf-166">Установка с помощью репозитория пакетов — Debian 9</span><span class="sxs-lookup"><span data-stu-id="c82cf-166">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="c82cf-167">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-167">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c82cf-168">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-168">This is the preferred method.</span></span>

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

<span data-ttu-id="c82cf-169">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.</span><span class="sxs-lookup"><span data-stu-id="c82cf-169">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="c82cf-170">Установка с помощью прямого скачивания — Debian 9</span><span class="sxs-lookup"><span data-stu-id="c82cf-170">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="c82cf-171">Скачивание пакета Debian</span><span class="sxs-lookup"><span data-stu-id="c82cf-171">Download the Debian package</span></span>
`powershell_6.2.0-1.debian.9_amd64.deb`
<span data-ttu-id="c82cf-172">со страницы [выпусков][] на компьютер с Debian.</span><span class="sxs-lookup"><span data-stu-id="c82cf-172">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="c82cf-173">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-173">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="c82cf-174">Удаление — Debian 9</span><span class="sxs-lookup"><span data-stu-id="c82cf-174">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="c82cf-175">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-175">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="c82cf-176">Этот пакет также работает в Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="c82cf-176">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="c82cf-177">Установка с помощью репозитория пакетов (рекомендуется) — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-177">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="c82cf-178">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c82cf-178">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c82cf-179">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo yum update powershell` для обновления PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-179">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="c82cf-180">Установка с помощью прямого скачивания — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-180">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="c82cf-181">Используя [CentOS 7][], скачайте пакет RPM</span><span class="sxs-lookup"><span data-stu-id="c82cf-181">Using [CentOS 7][], download the RPM package</span></span>
`powershell-6.2.0-1.rhel.7.x86_64.rpm`
<span data-ttu-id="c82cf-182">со страницы [выпусков][] на компьютер с CentOS.</span><span class="sxs-lookup"><span data-stu-id="c82cf-182">from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="c82cf-183">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-183">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c82cf-184">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="c82cf-184">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="c82cf-185">Удаление — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-185">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[<span data-ttu-id="c82cf-186">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-186">CentOS 7</span></span>]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c82cf-187">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-187">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c82cf-188">Установка с помощью репозитория пакетов (рекомендуется) — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-188">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="c82cf-189">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c82cf-189">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c82cf-190">Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo yum update powershell` для обновления PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-190">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c82cf-191">Установка с помощью прямого скачивания — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-191">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="c82cf-192">Скачивание пакета RPM</span><span class="sxs-lookup"><span data-stu-id="c82cf-192">Download the RPM package</span></span>
`powershell-6.2.0-1.rhel.7.x86_64.rpm`
<span data-ttu-id="c82cf-193">со страницы [выпусков][] на компьютер с Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="c82cf-193">from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="c82cf-194">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-194">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c82cf-195">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="c82cf-195">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c82cf-196">Удаление — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-196">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a><span data-ttu-id="c82cf-197">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c82cf-197">openSUSE</span></span>

### <a name="installation---opensuse-423"></a><span data-ttu-id="c82cf-198">Установка — openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c82cf-198">Installation - openSUSE 42.3</span></span>

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar libicu52_1

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.2.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.2.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.2.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="installation---opensuse-leap-15"></a><span data-ttu-id="c82cf-199">Установка — openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="c82cf-199">Installation - openSUSE Leap 15</span></span>

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar gzip libopenssl1_0_0 libicu60_2

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.2.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.2.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.2.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a><span data-ttu-id="c82cf-200">Удаление — openSUSE 42.3, openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="c82cf-200">Uninstallation - openSUSE 42.3, openSUSE Leap 15</span></span>

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a><span data-ttu-id="c82cf-201">Fedora</span><span class="sxs-lookup"><span data-stu-id="c82cf-201">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="c82cf-202">Fedora 28 поддерживается только в PowerShell Core 6.1 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="c82cf-202">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="c82cf-203">Установка с помощью репозитория пакетов (рекомендуется) — Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c82cf-203">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="c82cf-204">Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c82cf-204">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="c82cf-205">Установка с помощью прямого скачивания — Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c82cf-205">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="c82cf-206">Скачивание пакета RPM</span><span class="sxs-lookup"><span data-stu-id="c82cf-206">Download the RPM package</span></span>
`powershell-6.2.0-1.rhel.7.x86_64.rpm`
<span data-ttu-id="c82cf-207">со страницы [выпусков][] на компьютер с Fedora.</span><span class="sxs-lookup"><span data-stu-id="c82cf-207">from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="c82cf-208">Затем выполните в терминале следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c82cf-208">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c82cf-209">Кроме того, RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="c82cf-209">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="c82cf-210">Удаление — Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c82cf-210">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="c82cf-211">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="c82cf-211">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="c82cf-212">Поддержка Arch на этапе эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c82cf-212">Arch support is experimental.</span></span>

<span data-ttu-id="c82cf-213">PowerShell можно получить из пользовательского репозитория [Arch Linux][] (AUR).</span><span class="sxs-lookup"><span data-stu-id="c82cf-213">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="c82cf-214">Его можно скомпилировать с помощью [последнего выпуска с тегами][arch-release].</span><span class="sxs-lookup"><span data-stu-id="c82cf-214">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="c82cf-215">Его можно скомпилировать из [последней фиксации в основной репозиторий][arch-git].</span><span class="sxs-lookup"><span data-stu-id="c82cf-215">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="c82cf-216">Его можно установить с помощью [двоичного файла последнего выпуска][arch-bin].</span><span class="sxs-lookup"><span data-stu-id="c82cf-216">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="c82cf-217">Пакеты в AUR обслуживаются сообществом — официальная поддержка отсутствует.</span><span class="sxs-lookup"><span data-stu-id="c82cf-217">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="c82cf-218">Дополнительные сведения об установке пакетов из AUR см. на [вики-сайте Arch Linux](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) или в [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile) сообщества.</span><span class="sxs-lookup"><span data-stu-id="c82cf-218">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[<span data-ttu-id="c82cf-219">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="c82cf-219">Arch Linux</span></span>]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="c82cf-220">Snap-пакет</span><span class="sxs-lookup"><span data-stu-id="c82cf-220">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="c82cf-221">Установка Snap</span><span class="sxs-lookup"><span data-stu-id="c82cf-221">Getting snapd</span></span>

`snapd` <span data-ttu-id="c82cf-222">— это утилита для запуска Snap-пакетов.</span><span class="sxs-lookup"><span data-stu-id="c82cf-222">is required to run snaps.</span></span>
<span data-ttu-id="c82cf-223">Чтобы убедиться, что утилита `snapd` установлена, воспользуйтесь [этими инструкциями](https://docs.snapcraft.io/core/install).</span><span class="sxs-lookup"><span data-stu-id="c82cf-223">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="c82cf-224">Установка с использованием Snap</span><span class="sxs-lookup"><span data-stu-id="c82cf-224">Installation via Snap</span></span>

<span data-ttu-id="c82cf-225">Для упрощения установки (и обновления) PowerShell Core для Linux опубликован в [хранилище Snap](https://snapcraft.io/store).</span><span class="sxs-lookup"><span data-stu-id="c82cf-225">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="c82cf-226">Это предпочтительный метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-226">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

<span data-ttu-id="c82cf-227">Если вы хотите установить предварительную версию, используйте следующий метод.</span><span class="sxs-lookup"><span data-stu-id="c82cf-227">If you want to install preview version, use following method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="c82cf-228">После установки Snap будет автоматически обновлен, но вы можете активировать обновление с помощью `sudo snap refresh powershell` или `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="c82cf-228">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell` or `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="c82cf-229">Удаление</span><span class="sxs-lookup"><span data-stu-id="c82cf-229">Uninstallation</span></span>

```sh
sudo snap remove powershell
```

<span data-ttu-id="c82cf-230">или</span><span class="sxs-lookup"><span data-stu-id="c82cf-230">or</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a><span data-ttu-id="c82cf-231">Kali</span><span class="sxs-lookup"><span data-stu-id="c82cf-231">Kali</span></span>

### <a name="installation---kali"></a><span data-ttu-id="c82cf-232">Установка — Kali</span><span class="sxs-lookup"><span data-stu-id="c82cf-232">Installation - Kali</span></span>

```sh
# Download & Install prerequisites
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-9_amd64.deb
dpkg -i libicu57_57.1-9_amd64.deb
apt-get update && apt-get install -y curl gnupg apt-transport-https

# Add Microsoft public repository key to APT
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

# Add Microsoft package repository to the source list
echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" | tee /etc/apt/sources.list.d/powershell.list

# Install PowerShell package
apt-get update && apt-get install -y powershell

# Start PowerShell
pwsh
```

### <a name="uninstallation---kali"></a><span data-ttu-id="c82cf-233">Удаление — Kali</span><span class="sxs-lookup"><span data-stu-id="c82cf-233">Uninstallation - Kali</span></span>

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a><span data-ttu-id="c82cf-234">Raspbian</span><span class="sxs-lookup"><span data-stu-id="c82cf-234">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="c82cf-235">Поддержка Raspbian на этапе эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c82cf-235">Raspbian support is experimental.</span></span>

<span data-ttu-id="c82cf-236">Сейчас PowerShell поддерживается только в Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="c82cf-236">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="c82cf-237">Кроме того, CoreCLR (а соответственно и PowerShell Core) будет работать только на устройствах Pi 2 и Pi 3, в то время как в устройствах наподобие [Pi Zero](https://github.com/dotnet/coreclr/issues/10605) установлены процессоры, поддержка которых не предусмотрена.</span><span class="sxs-lookup"><span data-stu-id="c82cf-237">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="c82cf-238">Загрузите [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) и следуйте [инструкциям по установке](https://www.raspberrypi.org/documentation/installation/installing-images/README.md), чтобы установить его на свой Pi.</span><span class="sxs-lookup"><span data-stu-id="c82cf-238">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation---raspbian"></a><span data-ttu-id="c82cf-239">Установка — Raspbian</span><span class="sxs-lookup"><span data-stu-id="c82cf-239">Installation - Raspbian</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.2.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

<span data-ttu-id="c82cf-240">При необходимости можно создать символьную ссылку, позволяющую запустить PowerShell без указания пути к двоичному файлу pwsh</span><span class="sxs-lookup"><span data-stu-id="c82cf-240">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="c82cf-241">Удаление — Raspbian</span><span class="sxs-lookup"><span data-stu-id="c82cf-241">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="c82cf-242">Архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="c82cf-242">Binary Archives</span></span>

<span data-ttu-id="c82cf-243">Для поддержки расширенных сценариев развертывания на платформах Linux доступны архивы `tar.gz` двоичных файлов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-243">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="c82cf-244">Зависимости</span><span class="sxs-lookup"><span data-stu-id="c82cf-244">Dependencies</span></span>

<span data-ttu-id="c82cf-245">PowerShell создает переносимые двоичные файлы для всех дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="c82cf-245">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="c82cf-246">Однако среда выполнения .NET Core требует различные зависимости для разных дистрибутивов, и поэтому то же самое делает и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c82cf-246">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="c82cf-247">На следующей диаграмме показаны официально поддерживаемые зависимости .NET Core 2.0 для различных дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="c82cf-247">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="c82cf-248">ОС</span><span class="sxs-lookup"><span data-stu-id="c82cf-248">OS</span></span>                 | <span data-ttu-id="c82cf-249">Зависимости</span><span class="sxs-lookup"><span data-stu-id="c82cf-249">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="c82cf-250">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-250">Ubuntu 14.04</span></span>       | <span data-ttu-id="c82cf-251">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="c82cf-251">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c82cf-252">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="c82cf-252">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="c82cf-253">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-253">Ubuntu 16.04</span></span>       | <span data-ttu-id="c82cf-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="c82cf-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c82cf-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="c82cf-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="c82cf-256">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c82cf-256">Ubuntu 17.10</span></span>       | <span data-ttu-id="c82cf-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="c82cf-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c82cf-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="c82cf-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="c82cf-259">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c82cf-259">Ubuntu 18.04</span></span>       | <span data-ttu-id="c82cf-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="c82cf-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c82cf-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="c82cf-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="c82cf-262">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="c82cf-262">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="c82cf-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="c82cf-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c82cf-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="c82cf-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="c82cf-265">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="c82cf-265">Debian 9 (Stretch)</span></span> | <span data-ttu-id="c82cf-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="c82cf-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c82cf-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="c82cf-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="c82cf-268">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-268">CentOS 7</span></span> <br> <span data-ttu-id="c82cf-269">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-269">Oracle Linux 7</span></span> <br> <span data-ttu-id="c82cf-270">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="c82cf-270">RHEL 7</span></span> | <span data-ttu-id="c82cf-271">libunwind, libcurl, openssl-libs, libicu</span><span class="sxs-lookup"><span data-stu-id="c82cf-271">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="c82cf-272">openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c82cf-272">openSUSE 42.3</span></span> | <span data-ttu-id="c82cf-273">libcurl4, libopenssl1_0_0, libicu52_1</span><span class="sxs-lookup"><span data-stu-id="c82cf-273">libcurl4, libopenssl1_0_0, libicu52_1</span></span> |
| <span data-ttu-id="c82cf-274">openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="c82cf-274">openSUSE Leap 15</span></span> | <span data-ttu-id="c82cf-275">libcurl4, libopenssl1_0_0, libicu60_2</span><span class="sxs-lookup"><span data-stu-id="c82cf-275">libcurl4, libopenssl1_0_0, libicu60_2</span></span> |
| <span data-ttu-id="c82cf-276">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="c82cf-276">Fedora 27</span></span> <br> <span data-ttu-id="c82cf-277">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c82cf-277">Fedora 28</span></span> | <span data-ttu-id="c82cf-278">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="c82cf-278">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="c82cf-279">Чтобы развернуть двоичные файлы PowerShell в дистрибутивах Linux, для которых официальная поддержка не предусмотрена, необходимо специально установить необходимые пакеты, чтобы удовлетворить всем требованиям по зависимостям для целевой ОС.</span><span class="sxs-lookup"><span data-stu-id="c82cf-279">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="c82cf-280">Например, наш [Amazon Linux dockerfile][amazon-dockerfile] сначала устанавливает зависимости, а затем извлекает архив Linux `tar.gz`.</span><span class="sxs-lookup"><span data-stu-id="c82cf-280">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell-Docker/blob/master/release/community-stable/amazonlinux/docker/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="c82cf-281">Установка — архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="c82cf-281">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="c82cf-282">Linux</span><span class="sxs-lookup"><span data-stu-id="c82cf-282">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.2.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.2.0

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.2.0/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="c82cf-283">Удаление архивов двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="c82cf-283">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="c82cf-284">Пути</span><span class="sxs-lookup"><span data-stu-id="c82cf-284">Paths</span></span>

* `$PSHOME` <span data-ttu-id="c82cf-285">— это</span><span class="sxs-lookup"><span data-stu-id="c82cf-285">is</span></span> `/opt/microsoft/powershell/6.2.0/`
* <span data-ttu-id="c82cf-286">Профили пользователей будут считаны из</span><span class="sxs-lookup"><span data-stu-id="c82cf-286">User profiles will be read from</span></span> `~/.config/powershell/profile.ps1`
* <span data-ttu-id="c82cf-287">Профили по умолчанию будут считаны из</span><span class="sxs-lookup"><span data-stu-id="c82cf-287">Default profiles will be read from</span></span> `$PSHOME/profile.ps1`
* <span data-ttu-id="c82cf-288">Модули пользователей будут считаны из</span><span class="sxs-lookup"><span data-stu-id="c82cf-288">User modules will be read from</span></span> `~/.local/share/powershell/Modules`
* <span data-ttu-id="c82cf-289">Общие модули будут считаны из</span><span class="sxs-lookup"><span data-stu-id="c82cf-289">Shared modules will be read from</span></span> `/usr/local/share/powershell/Modules`
* <span data-ttu-id="c82cf-290">Модули по умолчанию будут считаны из</span><span class="sxs-lookup"><span data-stu-id="c82cf-290">Default modules will be read from</span></span> `$PSHOME/Modules`
* <span data-ttu-id="c82cf-291">Журнал PSReadline будет записан в</span><span class="sxs-lookup"><span data-stu-id="c82cf-291">PSReadline history will be recorded to</span></span> `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

<span data-ttu-id="c82cf-292">Профили учитывают конфигурацию PowerShell для отдельных узлов, поэтому профили конкретных узлов по умолчанию находятся в `Microsoft.PowerShell_profile.ps1` в тех же расположениях.</span><span class="sxs-lookup"><span data-stu-id="c82cf-292">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="c82cf-293">PowerShell отвечает требованиям [спецификации каталога размещения файлов, связанных со средой настольной графической среды (X-сервера), стандартизированного XDG (X Desktop Group)][xdg-bds] в Linux.</span><span class="sxs-lookup"><span data-stu-id="c82cf-293">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[<span data-ttu-id="c82cf-294">выпуски</span><span class="sxs-lookup"><span data-stu-id="c82cf-294">releases</span></span>]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
