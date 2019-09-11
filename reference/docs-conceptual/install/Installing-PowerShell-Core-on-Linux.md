---
title: Установка PowerShell Core в Linux
description: Сведения об установке PowerShell Core в различных дистрибутивах Linux
ms.date: 07/19/2019
ms.openlocfilehash: 7d7c9a9f915f0a6e735a7baec1ec56e9c205a155
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848182"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="6f1c8-103">Установка PowerShell Core в Linux</span><span class="sxs-lookup"><span data-stu-id="6f1c8-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="6f1c8-104">Поддерживается [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810], [Ubuntu 19.04][u1904], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora] и [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-104">Supports [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810], [Ubuntu 19.04][u1904], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="6f1c8-105">Для дистрибутивов Linux без официальной поддержки попробуйте установить PowerShell с помощью [соответствующего Snap-пакета][snap].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-105">For Linux distributions that aren't officially supported, you can try to install PowerShell using the [PowerShell Snap Package][snap].</span></span> <span data-ttu-id="6f1c8-106">Можно также попытаться развернуть двоичные файлы PowerShell напрямую с помощью [архива`tar.gz`][tar] Linux, но при этом нужно отдельно настроить необходимые зависимости с учетом операционной системы.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="6f1c8-107">Все пакеты доступны на нашей странице [выпусков][] GitHub.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-107">All packages are available on our GitHub [releases][] page.</span></span> <span data-ttu-id="6f1c8-108">После установки пакета запустите `pwsh` из терминала.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-108">After the package is installed, run `pwsh` from a terminal.</span></span>

[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[u1904]: #ubuntu-1904
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="6f1c8-109">Установка предварительных выпусков</span><span class="sxs-lookup"><span data-stu-id="6f1c8-109">Installing Preview Releases</span></span>

<span data-ttu-id="6f1c8-110">При установке предварительной версии PowerShell Core для Linux с помощью репозитория пакетов имя пакета меняется с `powershell` на `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="6f1c8-111">При установке с помощью прямого скачивания изменяется только имя файла.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-111">Installing via direct download doesn't change, other than the file name.</span></span>

<span data-ttu-id="6f1c8-112">В следующей таблице приведены команды для установки пакетов стабильной и предварительной версий с помощью различных диспетчеров пакетов:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-112">The following table contains the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="6f1c8-113">Дистрибутивы</span><span class="sxs-lookup"><span data-stu-id="6f1c8-113">Distribution(s)</span></span>|<span data-ttu-id="6f1c8-114">Команда стабильной версии</span><span class="sxs-lookup"><span data-stu-id="6f1c8-114">Stable Command</span></span> | <span data-ttu-id="6f1c8-115">Команда предварительной версии</span><span class="sxs-lookup"><span data-stu-id="6f1c8-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="6f1c8-116">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="6f1c8-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="6f1c8-117">CentOS, RedHat</span><span class="sxs-lookup"><span data-stu-id="6f1c8-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="6f1c8-118">Fedora</span><span class="sxs-lookup"><span data-stu-id="6f1c8-118">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1604"></a><span data-ttu-id="6f1c8-119">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-119">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="6f1c8-120">Установка с помощью репозитория пакетов — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-120">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="6f1c8-121">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-121">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="6f1c8-122">Предпочтительный метод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-122">The preferred method is as follows:</span></span>

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

<span data-ttu-id="6f1c8-123">В качестве суперпользователя однократно зарегистрируйте репозиторий Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-123">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="6f1c8-124">После регистрации можно обновить PowerShell с помощью `sudo apt-get upgrade powershell`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-124">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="6f1c8-125">Установка с помощью прямого скачивания — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-125">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="6f1c8-126">Скачайте пакет Debian `powershell_6.2.0-1.ubuntu.16.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-126">Download the Debian package `powershell_6.2.0-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="6f1c8-127">Затем выполните в терминале следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-127">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="6f1c8-128">Команда `dpkg -i` завершается ошибкой при наличии несопоставленных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-128">The `dpkg -i` command fails with unmet dependencies.</span></span> <span data-ttu-id="6f1c8-129">Следующая команда, `apt-get install -f`, разрешает эти ошибки и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-129">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="6f1c8-130">Удаление — Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-130">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="6f1c8-131">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-131">Ubuntu 18.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="6f1c8-132">Установка с помощью репозитория пакетов — Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-132">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="6f1c8-133">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-133">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="6f1c8-134">Предпочтительный метод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-134">The preferred method is as follows:</span></span>

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

<span data-ttu-id="6f1c8-135">В качестве суперпользователя однократно зарегистрируйте репозиторий Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-135">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="6f1c8-136">После регистрации можно обновить PowerShell с помощью `sudo apt-get upgrade powershell`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-136">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="6f1c8-137">Установка с помощью прямого скачивания — Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-137">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="6f1c8-138">Скачайте пакет Debian `powershell_6.2.0-1.ubuntu.18.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-138">Download the Debian package `powershell_6.2.0-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="6f1c8-139">Затем выполните в терминале следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-139">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="6f1c8-140">Команда `dpkg -i` завершается ошибкой при наличии несопоставленных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-140">The `dpkg -i` command fails with unmet dependencies.</span></span> <span data-ttu-id="6f1c8-141">Следующая команда, `apt-get install -f`, разрешает эти ошибки и завершает настройку пакета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-141">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="6f1c8-142">Удаление — Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-142">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="6f1c8-143">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="6f1c8-143">Ubuntu 18.10</span></span>

<span data-ttu-id="6f1c8-144">Поддерживается только установка с помощью `snapd`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-144">Installation is supported via `snapd`.</span></span> <span data-ttu-id="6f1c8-145">Инструкции см. в разделе о [snap-пакете][snap].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-145">For instructions, see [Snap Package][snap].</span></span>

> [!NOTE]
> <span data-ttu-id="6f1c8-146">Ubuntu 18.10 — [промежуточный выпуск](https://www.ubuntu.com/about/release-cycle), который [поддерживается сообществом](../powershell-support-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="6f1c8-146">Ubuntu 18.10 is an [interim release](https://www.ubuntu.com/about/release-cycle) that's [community supported](../powershell-support-lifecycle.md).</span></span>

## <a name="ubuntu-1904"></a><span data-ttu-id="6f1c8-147">Ubuntu 19.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-147">Ubuntu 19.04</span></span>

<span data-ttu-id="6f1c8-148">Поддерживается только установка с помощью `snapd`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-148">Installation is supported via `snapd`.</span></span> <span data-ttu-id="6f1c8-149">Инструкции см. в разделе о [snap-пакете][snap].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-149">For instructions, see [Snap Package][snap].</span></span>

> [!NOTE]
> <span data-ttu-id="6f1c8-150">Ubuntu 19.04 — [промежуточный выпуск](https://www.ubuntu.com/about/release-cycle), который [поддерживается сообществом](../powershell-support-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="6f1c8-150">Ubuntu 19.04 is an [interim release](https://www.ubuntu.com/about/release-cycle) that's [community supported](../powershell-support-lifecycle.md).</span></span>

## <a name="debian-8"></a><span data-ttu-id="6f1c8-151">Debian 8</span><span class="sxs-lookup"><span data-stu-id="6f1c8-151">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="6f1c8-152">Установка с помощью репозитория пакетов — Debian 8</span><span class="sxs-lookup"><span data-stu-id="6f1c8-152">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="6f1c8-153">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-153">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="6f1c8-154">Предпочтительный метод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-154">The preferred method is as follows:</span></span>

```sh
# Install system components
sudo apt-get update
sudo apt-get install -y curl apt-transport-https

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

<span data-ttu-id="6f1c8-155">В качестве суперпользователя однократно зарегистрируйте репозиторий Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-155">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="6f1c8-156">После регистрации можно обновить PowerShell с помощью `sudo apt-get upgrade powershell`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-156">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

## <a name="debian-9"></a><span data-ttu-id="6f1c8-157">Debian 9</span><span class="sxs-lookup"><span data-stu-id="6f1c8-157">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="6f1c8-158">Установка с помощью репозитория пакетов — Debian 9</span><span class="sxs-lookup"><span data-stu-id="6f1c8-158">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="6f1c8-159">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в репозиториях пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-159">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="6f1c8-160">Предпочтительный метод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-160">The preferred method is as follows:</span></span>

```sh
# Install system components
sudo apt-get update
sudo apt-get install -y curl gnupg apt-transport-https

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

<span data-ttu-id="6f1c8-161">В качестве суперпользователя однократно зарегистрируйте репозиторий Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-161">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="6f1c8-162">После регистрации можно обновить PowerShell с помощью `sudo apt-get upgrade powershell`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-162">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="6f1c8-163">Установка с помощью прямого скачивания — Debian 9</span><span class="sxs-lookup"><span data-stu-id="6f1c8-163">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="6f1c8-164">Скачайте пакет Debian `powershell_6.2.0-1.debian.9_amd64.deb` со страницы [выпусков][] на компьютер с Debian.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-164">Download the Debian package `powershell_6.2.0-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="6f1c8-165">Затем выполните в терминале следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-165">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="6f1c8-166">Удаление — Debian 9</span><span class="sxs-lookup"><span data-stu-id="6f1c8-166">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="6f1c8-167">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-167">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="6f1c8-168">Этот пакет работает в Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-168">This package works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="6f1c8-169">Установка с помощью репозитория пакетов (рекомендуется) — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-169">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="6f1c8-170">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-170">PowerShell Core for Linux is published to official Microsoft repositories for easy installation and updates.</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6f1c8-171">В качестве суперпользователя однократно зарегистрируйте репозиторий Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-171">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="6f1c8-172">После регистрации можно обновить PowerShell с помощью `sudo yum update powershell`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-172">After registration, you can update PowerShell with `sudo yum update powershell`.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="6f1c8-173">Установка с помощью прямого скачивания — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-173">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="6f1c8-174">Используя [CentOS 7][], скачайте пакет RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с CentOS.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-174">Using [CentOS 7][], download the RPM package `powershell-6.2.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="6f1c8-175">Затем выполните в терминале следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-175">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6f1c8-176">RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-176">You can install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="6f1c8-177">Удаление — CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-177">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6f1c8-179">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-179">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6f1c8-180">Установка с помощью репозитория пакетов (рекомендуется) — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-180">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="6f1c8-181">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-181">PowerShell Core for Linux is published to official Microsoft repositories for easy installation and updates.</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6f1c8-182">В качестве суперпользователя однократно зарегистрируйте репозиторий Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-182">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="6f1c8-183">После регистрации можно обновить PowerShell с помощью `sudo yum update powershell`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-183">After registration, you can update PowerShell with `sudo yum update powershell`.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6f1c8-184">Установка с помощью прямого скачивания — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-184">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="6f1c8-185">Скачайте пакет RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-185">Download the RPM package `powershell-6.2.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="6f1c8-186">Затем выполните в терминале следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-186">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6f1c8-187">RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-187">You can install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6f1c8-188">Удаление — Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-188">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a><span data-ttu-id="6f1c8-189">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6f1c8-189">openSUSE</span></span>

### <a name="installation---opensuse-423"></a><span data-ttu-id="6f1c8-190">Установка — openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="6f1c8-190">Installation - openSUSE 42.3</span></span>

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

### <a name="installation---opensuse-leap-15"></a><span data-ttu-id="6f1c8-191">Установка — openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="6f1c8-191">Installation - openSUSE Leap 15</span></span>

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

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a><span data-ttu-id="6f1c8-192">Удаление — openSUSE 42.3, openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="6f1c8-192">Uninstallation - openSUSE 42.3, openSUSE Leap 15</span></span>

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a><span data-ttu-id="6f1c8-193">Fedora</span><span class="sxs-lookup"><span data-stu-id="6f1c8-193">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="6f1c8-194">Fedora 28 поддерживается только в PowerShell Core 6.1 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-194">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="6f1c8-195">Установка с помощью репозитория пакетов (рекомендуется) — Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="6f1c8-195">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="6f1c8-196">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в официальных репозиториях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-196">PowerShell Core for Linux is published to official Microsoft repositories for easy installation and updates.</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="6f1c8-197">Установка с помощью прямого скачивания — Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="6f1c8-197">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="6f1c8-198">Скачайте пакет RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Fedora.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-198">Download the RPM package `powershell-6.2.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="6f1c8-199">Затем выполните в терминале следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-199">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6f1c8-200">RPM можно установить без промежуточного скачивания:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-200">You can install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="6f1c8-201">Удаление — Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="6f1c8-201">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="6f1c8-202">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="6f1c8-202">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="6f1c8-203">Поддержка Arch на этапе эксперимента.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-203">Arch support is experimental.</span></span>

<span data-ttu-id="6f1c8-204">PowerShell можно получить из пользовательского репозитория [Arch Linux][] (AUR).</span><span class="sxs-lookup"><span data-stu-id="6f1c8-204">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="6f1c8-205">Его можно скомпилировать с помощью [последнего выпуска с тегами][arch-release].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-205">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="6f1c8-206">Его можно скомпилировать из [последней фиксации в основной репозиторий][arch-git].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-206">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="6f1c8-207">Его можно установить с помощью [двоичного файла последнего выпуска][arch-bin].</span><span class="sxs-lookup"><span data-stu-id="6f1c8-207">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="6f1c8-208">Пакеты в AUR обслуживаются сообществом — официальная поддержка не предусмотрена.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-208">Packages in the AUR are community maintained; there's no official support.</span></span>

<span data-ttu-id="6f1c8-209">Дополнительные сведения об установке пакетов из AUR см. на [вики-сайте Arch Linux](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) или в [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile) сообщества.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-209">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="6f1c8-211">Snap-пакет</span><span class="sxs-lookup"><span data-stu-id="6f1c8-211">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="6f1c8-212">Установка Snap</span><span class="sxs-lookup"><span data-stu-id="6f1c8-212">Getting snapd</span></span>

<span data-ttu-id="6f1c8-213">Утилита `snapd` необходима для запуска snap-пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-213">`snapd` is required to run snaps.</span></span> <span data-ttu-id="6f1c8-214">Чтобы убедиться, что утилита `snapd` установлена, воспользуйтесь [этими инструкциями](https://docs.snapcraft.io/core/install).</span><span class="sxs-lookup"><span data-stu-id="6f1c8-214">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="6f1c8-215">Установка с использованием Snap</span><span class="sxs-lookup"><span data-stu-id="6f1c8-215">Installation via Snap</span></span>

<span data-ttu-id="6f1c8-216">Чтобы упростить установку и обновление, PowerShell Core для Linux публикуется в [хранилище Snap](https://snapcraft.io/store).</span><span class="sxs-lookup"><span data-stu-id="6f1c8-216">PowerShell Core for Linux is published to the [Snap store](https://snapcraft.io/store) for easy installation and updates.</span></span>

<span data-ttu-id="6f1c8-217">Предпочтительный метод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-217">The preferred method is as follows:</span></span>

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

<span data-ttu-id="6f1c8-218">Чтобы установить предварительную версию, используйте следующий метод:</span><span class="sxs-lookup"><span data-stu-id="6f1c8-218">To install a preview version, use the following method:</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="6f1c8-219">После установки Snap автоматически обновится.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-219">After installation, Snap will automatically upgrade.</span></span> <span data-ttu-id="6f1c8-220">Обновление можно активировать с помощью `sudo snap refresh powershell` или `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-220">You can trigger an upgrade using `sudo snap refresh powershell` or `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="6f1c8-221">Удаление</span><span class="sxs-lookup"><span data-stu-id="6f1c8-221">Uninstallation</span></span>

```sh
sudo snap remove powershell
```

<span data-ttu-id="6f1c8-222">или</span><span class="sxs-lookup"><span data-stu-id="6f1c8-222">or</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a><span data-ttu-id="6f1c8-223">Kali</span><span class="sxs-lookup"><span data-stu-id="6f1c8-223">Kali</span></span>

### <a name="installation---kali"></a><span data-ttu-id="6f1c8-224">Установка — Kali</span><span class="sxs-lookup"><span data-stu-id="6f1c8-224">Installation - Kali</span></span>

```sh
# Download & Install prerequisites
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-6+deb9u2_amd64.deb
dpkg -i libicu57_57.1-6+deb9u2_amd64.deb
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

### <a name="uninstallation---kali"></a><span data-ttu-id="6f1c8-225">Удаление — Kali</span><span class="sxs-lookup"><span data-stu-id="6f1c8-225">Uninstallation - Kali</span></span>

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a><span data-ttu-id="6f1c8-226">Raspbian</span><span class="sxs-lookup"><span data-stu-id="6f1c8-226">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="6f1c8-227">Поддержка Raspbian на этапе эксперимента.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-227">Raspbian support is experimental.</span></span>

<span data-ttu-id="6f1c8-228">Сейчас PowerShell поддерживается только в Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-228">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="6f1c8-229">CoreCLR и PowerShell Core будут работать только на устройствах Pi 2 и Pi 3. На таких устройствах, как [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), установлены процессоры, поддержка которых не предусмотрена.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-229">CoreCLR and PowerShell Core will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="6f1c8-230">Загрузите [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) и следуйте [инструкциям по установке](https://www.raspberrypi.org/documentation/installation/installing-images/README.md), чтобы установить его на свой Pi.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-230">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation---raspbian"></a><span data-ttu-id="6f1c8-231">Установка — Raspbian</span><span class="sxs-lookup"><span data-stu-id="6f1c8-231">Installation - Raspbian</span></span>

```sh
###################################
# Prerequisites

# Update package lists
sudo apt-get update

# Install libunwind8 and libssl1.0
# Regex is used to ensure that we do not install libssl1.0-dev, as it is a variant that is not required
sudo apt-get install '^libssl1.0.[0-9]$' libunwind8 -y

###################################
# Download and extract PowerShell

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.2.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

<span data-ttu-id="6f1c8-232">При необходимости можно создать символьную ссылку для запуска PowerShell без указания пути к двоичному файлу `pwsh`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-232">Optionally, you can create a symbolic link to start PowerShell without specifying the path to the `pwsh` binary.</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="6f1c8-233">Удаление — Raspbian</span><span class="sxs-lookup"><span data-stu-id="6f1c8-233">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="6f1c8-234">Архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="6f1c8-234">Binary Archives</span></span>

<span data-ttu-id="6f1c8-235">Для поддержки расширенных сценариев развертывания на платформах Linux доступны архивы `tar.gz` двоичных файлов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-235">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="6f1c8-236">Зависимости</span><span class="sxs-lookup"><span data-stu-id="6f1c8-236">Dependencies</span></span>

<span data-ttu-id="6f1c8-237">PowerShell создает переносимые двоичные файлы для всех дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-237">PowerShell builds portable binaries for all Linux distributions.</span></span> <span data-ttu-id="6f1c8-238">Но среда выполнения .NET Core, как и PowerShell, требует различные зависимости для разных дистрибутивов.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-238">But, .NET Core runtime requires different dependencies on different distributions, and PowerShell does too.</span></span>

<span data-ttu-id="6f1c8-239">На следующей диаграмме показаны официально поддерживаемые зависимости .NET Core 2.0 для различных дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-239">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="6f1c8-240">ОС</span><span class="sxs-lookup"><span data-stu-id="6f1c8-240">OS</span></span>                 | <span data-ttu-id="6f1c8-241">Зависимости</span><span class="sxs-lookup"><span data-stu-id="6f1c8-241">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="6f1c8-242">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-242">Ubuntu 16.04</span></span>       | <span data-ttu-id="6f1c8-243">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6f1c8-243">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6f1c8-244">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="6f1c8-244">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="6f1c8-245">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="6f1c8-245">Ubuntu 17.10</span></span>       | <span data-ttu-id="6f1c8-246">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6f1c8-246">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6f1c8-247">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="6f1c8-247">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="6f1c8-248">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="6f1c8-248">Ubuntu 18.04</span></span>       | <span data-ttu-id="6f1c8-249">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6f1c8-249">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6f1c8-250">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="6f1c8-250">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="6f1c8-251">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="6f1c8-251">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="6f1c8-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6f1c8-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6f1c8-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="6f1c8-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="6f1c8-254">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="6f1c8-254">Debian 9 (Stretch)</span></span> | <span data-ttu-id="6f1c8-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6f1c8-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6f1c8-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="6f1c8-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="6f1c8-257">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-257">CentOS 7</span></span> <br> <span data-ttu-id="6f1c8-258">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-258">Oracle Linux 7</span></span> <br> <span data-ttu-id="6f1c8-259">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="6f1c8-259">RHEL 7</span></span> | <span data-ttu-id="6f1c8-260">libunwind, libcurl, openssl-libs, libicu</span><span class="sxs-lookup"><span data-stu-id="6f1c8-260">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="6f1c8-261">openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="6f1c8-261">openSUSE 42.3</span></span> | <span data-ttu-id="6f1c8-262">libcurl4, libopenssl1_0_0, libicu52_1</span><span class="sxs-lookup"><span data-stu-id="6f1c8-262">libcurl4, libopenssl1_0_0, libicu52_1</span></span> |
| <span data-ttu-id="6f1c8-263">openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="6f1c8-263">openSUSE Leap 15</span></span> | <span data-ttu-id="6f1c8-264">libcurl4, libopenssl1_0_0, libicu60_2</span><span class="sxs-lookup"><span data-stu-id="6f1c8-264">libcurl4, libopenssl1_0_0, libicu60_2</span></span> |
| <span data-ttu-id="6f1c8-265">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="6f1c8-265">Fedora 27</span></span> <br> <span data-ttu-id="6f1c8-266">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="6f1c8-266">Fedora 28</span></span> | <span data-ttu-id="6f1c8-267">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="6f1c8-267">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="6f1c8-268">Чтобы развернуть двоичные файлы PowerShell в дистрибутивах Linux, для которых официальная поддержка не предусмотрена, необходимо специально установить необходимые пакеты, чтобы выполнить все требования, касающиеся зависимостей, для целевой ОС.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-268">To deploy PowerShell binaries on Linux distributions that aren't officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span> <span data-ttu-id="6f1c8-269">Например, наш [Dockerfile для Amazon Linux][amazon-dockerfile] сначала устанавливает зависимости, а затем извлекает архив Linux `tar.gz`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-269">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell-Docker/blob/master/release/community-stable/amazonlinux/docker/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="6f1c8-270">Установка — архивы двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="6f1c8-270">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="6f1c8-271">Linux</span><span class="sxs-lookup"><span data-stu-id="6f1c8-271">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="6f1c8-272">Удаление архивов двоичных файлов</span><span class="sxs-lookup"><span data-stu-id="6f1c8-272">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="6f1c8-273">Пути</span><span class="sxs-lookup"><span data-stu-id="6f1c8-273">Paths</span></span>

* <span data-ttu-id="6f1c8-274">`$PSHOME` имеет значение `/opt/microsoft/powershell/6.2.0/`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-274">`$PSHOME` is `/opt/microsoft/powershell/6.2.0/`</span></span>
* <span data-ttu-id="6f1c8-275">Профили пользователей будут считаны из `~/.config/powershell/profile.ps1`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-275">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="6f1c8-276">Профили по умолчанию будут считаны из `$PSHOME/profile.ps1`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-276">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="6f1c8-277">Модули пользователей будут считаны из `~/.local/share/powershell/Modules`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-277">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="6f1c8-278">Общие модули будут считаны из `/usr/local/share/powershell/Modules`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-278">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="6f1c8-279">Модули по умолчанию будут считаны из `$PSHOME/Modules`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-279">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="6f1c8-280">Журнал PSReadline будет записан в `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-280">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="6f1c8-281">Профили учитывают конфигурацию PowerShell для отдельных узлов, поэтому профили конкретных узлов по умолчанию находятся в `Microsoft.PowerShell_profile.ps1` в тех же расположениях.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-281">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="6f1c8-282">PowerShell отвечает требованиям [спецификации каталога размещения файлов, связанных со средой настольной графической среды (X-сервера), стандартизированного XDG (X Desktop Group)][xdg-bds] в Linux.</span><span class="sxs-lookup"><span data-stu-id="6f1c8-282">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[выпусков]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
