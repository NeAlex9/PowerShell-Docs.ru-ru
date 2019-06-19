---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Запуск подсистемы Windows PowerShell 2.0
ms.openlocfilehash: 824077008d2dcfd707e977d2112f0882d07a8aca
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030440"
---
# <a name="starting-the-windows-powershell-20-engine"></a>Запуск подсистемы Windows PowerShell 2.0

В этой статье объясняется, как запустить модуль Windows PowerShell 2.0 в Windows 8.1, Windows Server 2012 R2, Windows 8 и Windows Server 2012 с установленной подсистемой Windows PowerShell 2.0 и в других системах, в которых установлены Windows PowerShell 2.0, Windows PowerShell 3.0 и Windows PowerShell 4.0.

Windows PowerShell 4.0 и Windows PowerShell 3.0 предназначены для обратной совместимости с Windows PowerShell 2.0. Командлеты, поставщики, оснастки, модули и сценарии, написанные для Windows PowerShell 2.0, выполняются и в Windows PowerShell 4.0, и в Windows PowerShell 3.0 без изменений. Однако из-за изменений в политике активации среды выполнения в Microsoft .NET Framework 4 основные программы Windows PowerShell, написанные для Windows PowerShell 2.0 и скомпилированные с помощью среды CLR 2.0, не могут выполняться без изменения в Windows PowerShell 3.0 или Windows PowerShell 4.0, которые компилируются в среде CLR 4.0. Подсистема Windows PowerShell 2.0 предназначена для использования только в том случае, если выполнение существующего сценария или существующей основной программы невозможно из-за несовместимости с Windows PowerShell 4.0, Windows PowerShell 3.0 или Microsoft .NET Framework 4. Такие ситуации довольно редки.

Многие программы, требующие использования подсистемы Windows PowerShell 2.0, запускают ее автоматически. Эти инструкции предназначены для редких случаев, когда подсистему необходимо запустить вручную.

## <a name="installing-and-enabling-required-programs"></a>Установка и включение требуемых программ

Перед запуском подсистемы Windows PowerShell 2.0 включите подсистему Windows PowerShell 2.0 и Microsoft .NET Framework 3.5 с пакетом обновления 1. Инструкции см. в статье [Установка Windows PowerShell](../install/Installing-Windows-PowerShell.md).

Системы, где установлена Windows Management Framework 4.0 или Windows PowerShell 3.0, имеют все необходимые компоненты. Никакая дополнительная настройка не требуется. Дополнительные сведения об установке [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) или Windows PowerShell 3.0 см. в статье [Установка Windows PowerShell](../install/Installing-Windows-PowerShell.md).

## <a name="how-to-start-the-windows-powershell-20-engine"></a>Запуск подсистемы Windows PowerShell 2.0

При запуске Windows PowerShell по умолчанию открывается самая новая версия. Для запуска Windows PowerShell с подсистемой Windows PowerShell 2.0 используйте параметр Version в PowerShell.exe. Команду можно выполнить в любой командной строке, включая Windows PowerShell и Cmd.exe.

```
PowerShell.exe -Version 2
```

## <a name="how-to-start-a-remote-session-with-the-windows-powershell-20-engine"></a>Запуск удаленного сеанса с помощью подсистемы Windows PowerShell 2.0

Чтобы запустить подсистему Windows PowerShell 2.0 в удаленном сеансе, создайте его конфигурацию (которая также называется "конечной точкой") на удаленном компьютере, которая загружает подсистему Windows PowerShell 2.0. Конфигурация сеанса сохраняется на удаленном компьютере; любой авторизованный пользователь может использовать ее для создания сеансов на основе Windows PowerShell 2.0.

Это сложная задача, которая обычно выполняется системным администратором.

Следующая процедура использует параметр **PSVersion** командлета [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) для создания конфигурации сеанса с подсистемой Windows PowerShell 2.0. Можно также использовать параметр **PowerShellVersion** командлета [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866), чтобы создать файл конфигурации для сеанса, который загружает подсистему Windows PowerShell 2.0, и параметр **PSVersion** командлета [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea), чтобы изменить конфигурацию сеанса для использования подсистемы Windows PowerShell 2.0.

Дополнительные сведения о файлах конфигурации сеанса см. в статье [about_Session_Configuration_Files](https://technet.microsoft.com/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8). Сведения о конфигурациях сеанса, включая настройку и обеспечение безопасности, см. в статье [about_Session_Configurations[v4]](https://technet.microsoft.com/library/a2fbe12a-350c-4d04-be50-24102824e3ab).

#### <a name="to-start-a-remote-windows-powershell-20-session"></a>Запуск удаленного сеанса Windows PowerShell 2.0

1. Для создания конфигурации сеанса, требующей подсистемы Windows PowerShell 2.0 , используйте параметр **PSVersion** командлета [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) со значением "2.0". Выполните команду на компьютере на "стороне сервера" или на принимающей стороне подключения.

   Следующий пример команды создает конфигурацию сеанса PS2 на компьютере Server01. Чтобы выполнить эту команду, запустите Windows PowerShell 4.0 или Windows PowerShell 3.0 с параметром **Запуск от имени администратора**.

   ```powershell
   Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
   ```

2. Чтобы создать на компьютере Server01 сеанс, использующий конфигурацию сеанса PS2, примените параметр **ConfigurationName** для командлетов, создающих удаленный сеанс, таких как [New-PSSession](https://technet.microsoft.com/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f).

   При запуске сеанса, использующего конфигурацию, подсистема Windows PowerShell 2.0 автоматически загружается в него.

   Следующая команда запускает сеанс на компьютере Server01, который использует конфигурацию PS2. Сеанс сохраняется в переменную $s.

   ```powershell
   $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
   ```

## <a name="how-to-start-a-background-job-with-the-windows-powershell-20-engine"></a>Запуск фонового задания с помощью подсистемы Windows PowerShell 2.0

Чтобы запустить фоновое задание с помощью подсистемы Windows PowerShell 2.0, используйте параметр **PSVersion** командлета [Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442).

Следующая команда запускает фоновое задание с помощью подсистемы Windows PowerShell 2.0:

```powershell
Start-Job {Get-Process} -PSVersion 2.0
```

Дополнительные сведения о фоновых заданиях см. в разделе [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).
