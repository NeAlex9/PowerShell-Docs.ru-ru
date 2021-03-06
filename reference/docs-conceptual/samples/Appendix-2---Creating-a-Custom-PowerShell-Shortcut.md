---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Приложение 2. Создание настраиваемого ярлыка PowerShell
description: Следующая процедура описывает создание ярлыка для Windows PowerShell, в котором уже заданы нужные параметры.
ms.openlocfilehash: abdab517dec1357050bf431b6f2e35311ad49976
ms.sourcegitcommit: 9080316e3ca4f11d83067b41351531672b667b7a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92500731"
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a>Приложение 2. Создание настраиваемого ярлыка PowerShell

Следующая процедура описывает создание ярлыка для Windows PowerShell, в котором уже заданы нужные параметры.

1. Создайте ярлык, указывающий на Powershell.exe.

1. Щелкните его правой кнопкой мыши и выберите пункт **Свойства** .

1. Откройте вкладку **Параметры** .

1. В разделе **Правка** установите флажок **Для выделения** .

    Этот параметр позволяет выбрать текст в окне консоли Windows PowerShell, перетащив курсор при нажатой левой кнопке мыши, а также скопировать текст в буфер обмена, нажав клавишу ВВОД или правую кнопку мыши.

1. В разделе **Правка** установите флажок **Быстрая вставка** . Этот параметр позволяет автоматически вставить текст из буфера обмена с помощью щелчка правой кнопкой мыши в окне консоли.

1. В поле **Размер буфера** раздела **Запоминание команд** введите или выберите число от 1 до 999. Это задает число введенных команд, которые сохраняются в буфере консоли.

1. В разделе **Запоминание команд** установите флажок **Отбрасывать повторения** , чтобы исключить повторяющиеся команды из буфера консоли.

1. Откройте вкладку **Расположение** .

1. В поле **Высота** раздела **Screen Buffer** (Буфер экрана) введите число от 1 до 9999. Высота обозначает число строк выходных данных, помещаемых в буфер. Это максимальное число строк, сохраняемых для просмотра при прокрутке в окне консоли. Если это число меньше высоты, отображаемой в разделе **Размер окна** , высота окна автоматически уменьшается до того же значения.

1. В разделе **Размер окна** введите число от 1 до 9999 для ширины. Оно представляет число символов, отображаемых в окне консоли. По умолчанию ширина равна 80, и именно на нее рассчитано форматирование выходных данных Windows PowerShell.

1. Если вы хотите, чтобы при открытии консоль располагалась в определенной точке на рабочем столе, снимите флажок **Автоматический выбор** в разделе **Положение окна** , а затем измените значения в полях **Слева** и **Сверху** раздела **Положение окна** .

1. Нажмите кнопку **ОК** .
