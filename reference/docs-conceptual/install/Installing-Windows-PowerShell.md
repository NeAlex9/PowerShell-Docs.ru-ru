---
ms.date: 08/09/2017
keywords: powershell, cmdlet, командлет, download, скачать, install, установить, setup, установка, windows 10, windows 8.1, windows 8.0, windows 7
title: Установка Windows PowerShell
ms.openlocfilehash: 345cde8012bece730e7217ed16be6175ad26bb28
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "62086482"
---
# <a name="installing-windows-powershell"></a>Установка Windows PowerShell

Windows PowerShell установлен по умолчанию в каждой ОС Windows, начиная с Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1).

Если вас интересует PowerShell версии 6 или более поздней, вам нужно установить PowerShell Core вместо Windows PowerShell. Дополнительные сведения см. в статье [Установка PowerShell Core в Windows](Installing-PowerShell-Core-on-Windows.md).

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a>Поиск PowerShell в Windows 10, 8.1, 8.0 и 7

Иногда найти консоль или ISE (интегрированную среду сценариев) PowerShell в Windows бывает непросто, так как их расположение в разных версиях Windows отличается.

Следующие таблицы помогут найти PowerShell в вашей версии Windows.
Все указанные версии являются оригинальными, сразу после выпуска и без обновлений.

### <a name="for-console"></a>Консоль

Версия | Location
-- | --
Windows 10 | Щелкните значок Windows в левом нижнем углу и начните вводить PowerShell.
Windows 8.1, 8.0 | На начальном экране начните вводить PowerShell.<br/>Если вы находитесь на рабочем столе, щелкните значок Windows в левом нижнем углу и начните вводить PowerShell.
Windows 7 с пакетом обновления 1 (SP1) | Щелкните значок Windows в левом нижнем углу и в поле поиска начните вводить PowerShell.

### <a name="for-ise"></a>ISE

Версия | Location
-- | --
Windows 10 | Щелкните значок Windows в левом нижнем углу и начните вводить ISE.
Windows 8.1, 8.0 | На начальном экране введите **PowerShell ISE**.<br/>Если вы находитесь на рабочем столе, щелкните значок Windows в левом нижнем углу и введите **PowerShell ISE**.
Windows 7 с пакетом обновления 1 (SP1) | Щелкните значок Windows в левом нижнем углу и в поле поиска начните вводить PowerShell.

## <a name="finding-powershell-in-windows-server-versions"></a>Поиск PowerShell в версиях Windows Server

Начиная с Windows Server 2008 R2, операционную систему Windows можно установить без графического пользовательского интерфейса (GUI).
Выпуски Windows Server без GUI называются выпусками **Core**, а выпуски с GUI — **Desktop**.

### <a name="windows-server-core-editions"></a>Выпуски Windows Server Core

Во всех выпусках Core при входе на сервер открывается окно командной строки Windows.

Введите `powershell` и нажмите клавишу **ВВОД**, чтобы запустить PowerShell в сеансе командной строки.
Введите `exit`, чтобы завершить сеанс PowerShell и вернуться к командной строке.

### <a name="windows-server-desktop-editions"></a>Выпуски Windows Server Desktop

Во всех выпусках Desktop нужно щелкнуть значок Windows в левом нижнем углу и начать вводить PowerShell.
Появятся параметры консоли и ISE.

Единственное исключение из этого правила — ISE в Windows Server 2008 R2 с пакетом обновления 1 (SP1). В этом случае щелкните значок Windows в левом нижнем углу и введите PowerShell ISE.

## <a name="how-to-check-the-version-of-powershell"></a>Проверка версии PowerShell

Чтобы узнать, какая версия PowerShell установлена, запустите консоль PowerShell (или ISE), введите `$PSVersionTable` и нажмите клавишу **ВВОД**. Найдите значение `PSVersion`.

## <a name="upgrading-existing-windows-powershell"></a>Обновление существующей версии Windows PowerShell

В пакет установки для PowerShell входит установщик WMF.
Версия установщика WMF совпадает с версией PowerShell. Для Windows PowerShell нет отдельного установщика.

Если вам нужно обновить существующую версию PowerShell, в Windows используйте следующую таблицу, чтобы найти установщик для нужной версии PowerShell.

Windows | PS 3.0 | PS 4.0 | PS 5.0 | PS 5.1 |
--|--|--|--|--|
Windows 10 (см. примечание 1)<br/>Windows Server 2016 | - | - | - | установлено
Windows 8.1<br/>Windows Server 2012 R2 | - | установлено | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 8<br/>Windows Server 2012 | установлено | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 7 с пакетом обновления 1 (SP1)<br/>Windows Server 2008 R2 с пакетом обновления 1 (SP1) | [WMF 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> [!NOTE]
>
> Если в начальном выпуске Windows 10 включены автоматические обновления, PowerShell обновляется с версии 5.0 до 5.1.
>
> Если оригинальная версия Windows 10 не обновлена в Центре обновления Windows, версия PowerShell будет 5.0.

## <a name="need-azure-powershell"></a>Необходимость Azure PowerShell

Если вы ищете **Azure PowerShell**, можно начать с раздела [Общие сведения об Azure PowerShell](/powershell/azure/overview).

Либо вам нужен раздел [Установка и настройка Azure PowerShell](/powershell/azure/install-az-ps)

## <a name="see-also"></a>См. также:

[Требования Windows PowerShell к системе](Windows-PowerShell-System-Requirements.md)

[Запуск Windows PowerShell](../getting-started/Starting-Windows-PowerShell.md)
