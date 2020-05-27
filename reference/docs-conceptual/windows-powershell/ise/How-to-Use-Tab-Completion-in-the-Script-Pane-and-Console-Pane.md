---
ms.date: 01/02/2020
keywords: powershell,командлет
title: Использование заполнения нажатием клавиши TAB в областях сценариев и консоли
ms.openlocfilehash: 07cf9ff75db8d33ed018542153bfcd7503035e40
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83808830"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Использование заполнения нажатием клавиши TAB в областях сценариев и консоли

Заполнение нажатием клавиши TAB предоставляет автоматическую справку при вводе в области скриптов или команд. Чтобы воспользоваться этой функцией, выполните следующие действия:

## <a name="to-automatically-complete-a-command-entry"></a>Автоматическое завершение ввода команды

В области команд или сценариев введите несколько символов команды и нажмите клавишу <kbd>TAB</kbd>, чтобы выбрать нужный текст завершения. Если с изначально введенного текста начинается несколько элементов, нажимайте клавишу <kbd>TAB</kbd>, пока не появится нужный. Заполнение нажатием клавиши TAB позволяет ввести имя командлета, параметра, переменной, свойства объекта или путь к файлу.

> [!NOTE]
> В области сценариев нажатие клавиши <kbd>TAB</kbd> автоматически завершает команду только при редактировании файлов `.ps1`, `.psd1` или `.psm1`. Заполнение нажатием клавиши TAB работает в любое время при вводе в области команд.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>Автоматическое завершение ввода для параметра командлета

В области команд или сценариев введите командлет, поставьте после него дефис и нажмите клавишу <kbd>TAB</kbd>.

Например, введите `Get-Process -` и нажмите клавишу <kbd>TAB</kbd> несколько раз для отображения параметров командлета по очереди.

## <a name="see-also"></a>См. также:

- [Введение в интегрированную среду сценариев Windows PowerShell](Introducing-the-Windows-PowerShell-ISE.md)
- [Создание вкладки PowerShell](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)