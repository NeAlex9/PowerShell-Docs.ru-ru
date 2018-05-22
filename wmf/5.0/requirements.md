---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: ce68bc57a5da049cf895165420ba7c4e21b3e63b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="system-requirements"></a>Системные требования

- Перед установкой WMF 5.0 RTM установите последние обновления для Windows.
- WMF 5.0 RTM работает только в следующих операционных системах:

    | Операционная система       | Выпуски         | Необходимые компоненты        |  Ссылки на пакеты |
    |------------------------|--------------|------------------|----------------------| --------------|
    | Windows Server 2012 R2 |  |  | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
    | Windows Server 2012    |  |  | [W2K12-KB3134759-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) |
    | Windows Server 2008 R2 с пакетом обновления 1 (SP1) | Все, кроме IA64 | Установлена платформа [.NET Framework 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) и [.NET Framework 4.5 или выше](https://msdn.microsoft.com/library/5a4x27ek.aspx).| [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)|
    | Windows 8.1 | Профессиональная, Корпоративная | | **x64:**  [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) </br> **x86:**  [Win8.1-KB3134758-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963)|
    | Windows 7 с пакетом обновления 1 (SP1) | all | Установлена платформа [.NET Framework 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) и [.NET Framework 4.5 или выше](https://msdn.microsoft.com/library/5a4x27ek.aspx). | **x64:**  [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)  </br> **x86:**  [Win7-KB3134760-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962)|

# <a name="installation-instructions"></a>Инструкции по установке

### <a name="to-install-wmf-50-from-windows-explorer-or-file-explorer"></a>Установка WMF 5.0 из проводника Windows Explorer (или File Explorer):

1. Перейдите в папку, куда был скачан MSU-файл.

2. Дважды щелкните этот файл для его запуска.

### <a name="to-install-wmf-50-from-command-prompt"></a>Установка WMF 5.0 из командной строки:

1. После скачивания подходящего пакета для архитектуры вашего компьютера откройте окно командной строки с повышенными правами (используйте "Запуск от имени администратора"). В установке основных серверных компонентов для Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 с пакетом обновления 1 (SP1) командная строка по умолчанию открывается с повышенными правами.

2. Перейдите в папку, куда был скачан или скопирован пакет установки WMF 5.0.

3. Выполните одну из следующих команд:
    - На компьютерах под управлением Windows Server 2012 R2 или Windows 8.1 (x64) запустите **Win8.1AndW2K12R2-KB3134758-x64.msu /quiet**.
    - На компьютерах под управлением Windows Server 2012 запустите **W2K12-KB3134759-x64.msu /quiet**.
    - На компьютерах под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) (x64) запустите **Win7AndW2K8R2-KB3134760-x64.msu /quiet**.
    - На компьютерах под управлением Windows 8.1 (x86) запустите **Win8.1-KB3134758-x86.msu /quiet**.
    - На компьютерах под управлением Windows 7 с пакетом обновления 1 (SP1) (x86) запустите **Win7-KB3134760-x86.msu /quiet**.

### <a name="additional-installation-notes-for-windows-server-2008-r2-sp1-and-windows-7-sp1"></a>Дополнительные замечания по установке для Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1):

Убедитесь, что выполнены следующие предварительные условия.
- Установлен самый последний пакет обновления.
- Установлен [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855).
- Установлена [платформа .NET Framework 4.5 или более ранней версии](https://msdn.microsoft.com/library/5a4x27ek.aspx).

**Зависимость WMF 4.0**

Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1) содержат встроенные PowerShell 2.0, WinRM и WMI. Пакеты WMF 3.0 и WMF 4.0, которые обновляют эти встроенные компоненты, были выпущены после выпуска Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1). При установке или удалении пакетов WMF 3.0 и WMF 4.0 были выявлены некоторые проблемы при следующих вариантах обновления:

- Встроенные методы --> WMF 4.0.
- Встроенные методы --> WMF 3.0--> WMF4.0.

Все эти проблемы были устранены в пакетах WMF 4.0. Таким образом, для установки WMF 5.0 в системе Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) в ней должен быть установлен WMF 4.0. Ниже приведены конкретные проблемы, которые могут возникнуть при установке WMF 4.0 перед обновлением до WMF 5.0.

- Журнал перенаправленных событий недоступен, и журнал EventCollector не отображается в окне просмотра событий после удаления WMF 3.0 или WMF 5.0 (без предварительной установки WMF 4.0) в Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1) ([KB2809215](https://support.microsoft.com/en-us/kb/2809215)).
- Установленное значение переменной среды *PSModulePath* сбрасывается в значение по умолчанию при обновлении до WMF 5.0 напрямую из встроенного PowerShell 2.0 ([KB2872035](https://support.microsoft.com/en-us/kb/2872035)) или при обновлении с WMF 3.0 до WMF 5.0. ([KB2872047](https://support.microsoft.com/en-us/kb/2872047)) в Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1).

**Зависимость WinRM**

Служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM. По умолчанию WinRM не включена в Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1). Чтобы включить WinRM, запустите **Set-WSManQuickConfig** в сеансе с повышенными привилегиями Windows PowerShell.

# <a name="uninstallation-instructions"></a>Инструкции по удалению

### <a name="using-command-prompt"></a>Использование командной строки

1.  Откройте окно **Командная строка**.

2.  Запустите [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) (Автономное средство запуска Центра обновления Windows), как показано ниже:

В Windows Server 2012 R2 и Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
В Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
В Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1):
```powershell
wusa /uninstall /kb:3134760
```

### <a name="using-control-panel"></a>Использование панели управления

1.  Откройте **Панель управления**.

2.  Откройте **Программы** и выберите **Удаление программы**.

3.  Щелкните **Просмотр установленных обновлений**.

4.  Выберите **Windows Management Framework 5.0** в списке установленных обновлений. Это соответствует *KB3134758*, *KB3134759* или *KB3134760*. Щелкните **Удалить**.
