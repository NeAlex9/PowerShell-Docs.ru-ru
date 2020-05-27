---
ms.date: 01/02/2020
keywords: powershell,командлет
title: Сочетания клавиш для интегрированной среды сценариев Windows PowerShell
ms.openlocfilehash: ee1b5961f8528d44330345bc49368e61970861ca
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809770"
---
# <a name="keyboard-shortcuts-for-the-windows-powershell-ise"></a>Сочетания клавиш для интегрированной среды сценариев Windows PowerShell

Используйте следующие сочетания клавиш для выполнения действий в интегрированной среде скриптов Windows PowerShell®. Интегрированная среда сценариев Windows PowerShell доступна в серверных и клиентских операционных системах Windows, но ее можно установить и в некоторых старых операционных системах Windows в составе [скачиваемого пакета Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881).

## <a name="keyboard-shortcuts-for-editing-text"></a>Сочетания клавиш для редактирования текста

При редактировании текста можно использовать приведенные ниже сочетания клавиш.

|              Действие              |       Сочетания клавиш       |                                                                                                                                                 Область использования                                                                                                                                                 |
| -------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Help** (Справка)                         | <kbd>F1</kbd>                  | Область сценариев **Важно!** Можно указать, что информация, выдаваемая при нажатии клавиши <kbd>F1</kbd>, предоставляется из библиотеки TechNet в Интернете или скачанной справки (см. описание `Update-Help`). Для выбора щелкните **Tools** (Инструменты), **Options** (Параметры), а затем на вкладке **General Settings** (Общие параметры) установите или снимите флажок **Use local help content instead of online content** (Использовать локальную справку вместо справки в Интернете). |
| **Copy**.                         | <kbd>CTRL</kbd>+<kbd>C</kbd>   | Область сценариев, область команд, область вывода                                                                                                                                                                                                                                                                 |
| **Вырезать**                          | <kbd>CTRL</kbd>+<kbd>X</kbd>   | Область сценариев, область команд                                                                                                                                                                                                                                                                              |
| **Развертывание или свертывание структуры** | <kbd>CTRL</kbd>+<kbd>M</kbd>   | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Поиск в сценарии**               | <kbd>CTRL</kbd>+<kbd>F</kbd>   | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Поиск следующего элемента в сценарии**          | <kbd>F3</kbd>                  | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Поиск предыдущего элемента в сценарии**      | <kbd>SHIFT</kbd>+<kbd>F3</kbd> | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Поиск парной фигурной скобки**          | <kbd>CTRL</kbd>+<kbd>]</kbd>   | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Вставить**                        | <kbd>CTRL</kbd>+<kbd>V</kbd>   | Область сценариев, область команд                                                                                                                                                                                                                                                                              |
| **Повторить**                         | <kbd>CTRL</kbd>+<kbd>Y</kbd>   | Область сценариев, область команд                                                                                                                                                                                                                                                                              |
| **Заменить в сценарии**            | <kbd>CTRL</kbd>+<kbd>H</kbd>   | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Сохранить**                         | <kbd>CTRL</kbd>+<kbd>S</kbd>   | Область сценариев                                                                                                                                                                                                                                                                                            |
| **Выделить все**                   | <kbd>CTRL</kbd>+<kbd>A</kbd>   | Область сценариев, область команд, область вывода                                                                                                                                                                                                                                                                 |
| **Отображение фрагментов кода**                | <kbd>CTRL</kbd>+<kbd>J</kbd>   | Область сценариев, область команд                                                                                                                                                                                                                                                                              |
| **Отменить**                         | <kbd>CTRL</kbd>+<kbd>Z</kbd>   | Область сценариев, область команд                                                                                                                                                                                                                                                                              |

## <a name="keyboard-shortcuts-for-running-scripts"></a>Сочетания клавиш для выполнения сценариев

При запуске сценариев в области сценариев можно использовать приведенные ниже сочетания клавиш.

|            Действие            |                                                                                                             Сочетание клавиш                                                                                                             |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Создать**                      | <kbd>CTRL</kbd>+<kbd>N</kbd>                                                                                                                                                                                                              |
| **Открыть**                     | <kbd>CTRL</kbd>+<kbd>O</kbd>                                                                                                                                                                                                              |
| **Выполнить**                      | <kbd>F5</kbd>                                                                                                                                                                                                                             |
| **Запуск выбранного**            | <kbd>F8</kbd>                                                                                                                                                                                                                             |
| **Остановить выполнение**           | <kbd>CTRL</kbd>+<kbd>BREAK</kbd>. Клавиши <kbd>CTRL</kbd>+<kbd>C</kbd> можно использовать при однозначном контексте (при отсутствии выбранного текста).                                                                                              |
| **Переход** (к следующему сценарию)     | <kbd>CTRL</kbd>+<kbd>TAB</kbd> **Примечание.** Переход к следующему скрипту работает только в том случае, если открыта одна вкладка Windows PowerShell или открыто несколько вкладок Windows PowerShell и фокус находится в области скриптов.               |
| **Переход** (к предыдущему сценарию) | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>TAB</kbd> **Примечание.** Переход к предыдущему скрипту работает только в том случае, если открыта одна вкладка Windows PowerShell или открыто несколько вкладок Windows PowerShell и фокус находится в области скриптов. |

## <a name="keyboard-shortcuts-for-customizing-the-view"></a>Сочетания клавиш для настройки представления

Для настройки представления в интегрированной среде сценариев Windows PowerShell можно использовать приведенные ниже сочетания клавиш. Они доступны во всех областях приложения.

|                        Действие                         |               Сочетание клавиш               |
| ----------------------------------------------------- | --------------------------------------------- |
| **Переход в область команд (версия 2) или консоли (версия 3 и более поздние)** | <kbd>CTRL</kbd>+<kbd>D</kbd>                  |
| **Переход в область вывода (версия 2)**                       | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>O</kbd> |
| **Перейти в область сценариев**                                 | <kbd>CTRL</kbd>+<kbd>I</kbd>                  |
| **Показать область сценариев**                                  | <kbd>CTRL</kbd>+<kbd>R</kbd>                  |
| **Скрыть область сценариев**                                  | <kbd>CTRL</kbd>+<kbd>R</kbd>                  |
| **Переместить область сценариев вверх**                               | <kbd>CTRL</kbd>+<kbd>1</kbd>                  |
| **Переместить область сценариев вправо**                            | <kbd>CTRL</kbd>+<kbd>2</kbd>                  |
| **Развернуть область сценариев**                              | <kbd>CTRL</kbd>+<kbd>3</kbd>                  |
| **Увеличить**                                           | <kbd>CTRL</kbd>+<kbd>+</kbd>                  |
| **Уменьшить**                                          | <kbd>CTRL</kbd>+<kbd>-</kbd>                  |

## <a name="keyboard-shortcuts-for-debugging-scripts"></a>Сочетания клавиш для отладки сценариев

При отладке сценариев можно использовать приведенные ниже сочетания клавиш.

|           Действие           |               Сочетание клавиш                |                Область использования                |
| -------------------------- | ---------------------------------------------- | ------------------------------------ |
| **Запустить или продолжить**           | <kbd>F5</kbd>                                  | Область сценариев при отладке сценария |
| **Шаг с заходом**              | <kbd>F11</kbd>                                 | Область сценариев при отладке сценария |
| **Шаг с обходом**              | <kbd>F10</kbd>                                 | Область сценариев при отладке сценария |
| **Шаг с выходом**               | <kbd>SHIFT</kbd>+<kbd><kbd>F11</kbd></kbd>     | Область сценариев при отладке сценария |
| **Отображение стека вызовов**     | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>D</kbd>  | Область сценариев при отладке сценария |
| **Список точек останова**       | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>L</kbd>  | Область сценариев при отладке сценария |
| **Переключить точку останова**      | <kbd>F9</kbd>                                  | Область сценариев при отладке сценария |
| **Удалить все точки останова** | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>F9</kbd> | Область сценариев при отладке сценария |
| **Остановить отладчик**          | <kbd>SHIFT</kbd>+<kbd>F5</kbd>                 | Область сценариев при отладке сценария |

> [!NOTE]
> При отладке сценариев в интегрированной среде сценариев Windows PowerShell также можно использовать сочетания клавиш, предназначенные для консоли Windows PowerShell. Для этого необходимо ввести ярлык в области команд и нажать клавишу <kbd>ВВОД</kbd>.

|                        Действие                        | Сочетание клавиш |                Область использования                 |
| ---------------------------------------------------- | ----------------- | ------------------------------------- |
| **Продолжить**                                         | `C`               | Область консоли при отладке сценария |
| **Шаг с заходом**                                        | `S`               | Область консоли при отладке сценария |
| **Шаг с обходом**                                        | `V`               | Область консоли при отладке сценария |
| **Шаг с выходом**                                         | `O`               | Область консоли при отладке сценария |
| **Повтор последней команды** (для шага с заходом или шага с обходом) | <kbd>ВВОД</kbd>  | Область консоли при отладке сценария |
| **Отображение стека вызовов**                               | `K`               | Область консоли при отладке сценария |
| **Остановить отладку**                                   | `Q`               | Область консоли при отладке сценария |
| **Вывести сценарий**                                  | `L`               | Область консоли при отладке сценария |
| **Отобразить команды отладки для консоли**               | `H` либо `?`        | Область консоли при отладке сценария |

## <a name="keyboard-shortcuts-for-windows-powershell-tabs"></a>Сочетания клавиш для вкладок сценариев Windows PowerShell

При работе с вкладками Windows PowerShell можно использовать приведенные ниже сочетания клавиш.

|             Действие              |                                                        Сочетание клавиш                                                        |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Закрыть вкладку PowerShell**        | <kbd>CTRL</kbd>+<kbd>W</kbd>                                                                                                    |
| **Создать вкладку PowerShell**          | <kbd>CTRL</kbd>+<kbd>T</kbd>                                                                                                    |
| **Предыдущая вкладка PowerShell**     | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>TAB</kbd>. Это сочетание клавиш работает только в том случае, если на вкладках Windows PowerShell нет открытых файлов. |
| **Следующая вкладка Windows PowerShell** | <kbd>CTRL</kbd>+<kbd>TAB</kbd>. Это сочетание клавиш работает только в том случае, если на вкладках Windows PowerShell нет открытых файлов.                  |

## <a name="keyboard-shortcuts-for-starting-and-exiting"></a>Сочетания клавиш для запуска и выхода

Для запуска консоли PowerShell (PowerShell.exe) или выхода из интегрированной среды сценариев Windows PowerShell можно использовать приведенные ниже сочетания клавиш.

|                        Действие                        |               Сочетание клавиш               |
| ---------------------------------------------------- | --------------------------------------------- |
| **Выйти**                                             | <kbd>ALT</kbd>+<kbd>F4</kbd>                  |
| **Запуск PowerShell.exe** (консоль Windows PowerShell) | <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>P</kbd> |

## <a name="see-also"></a>См. также:

- [PowerShell Magazine: The Complete List of Windows PowerShell ISE Keyboard Shortcuts](https://www.powershellmagazine.com/2013/01/29/the-complete-list-of-powershell-ise-3-0-keyboard-shortcuts/) (Журнал PowerShell: полный список сочетаний клавиш для интегрированной среды сценариев Windows PowerShell)