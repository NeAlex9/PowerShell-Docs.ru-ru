---
ms.date: 09/13/2016
ms.topic: reference
title: Примеры пользовательских узлов
description: Примеры пользовательских узлов
ms.openlocfilehash: 939b9f5d6bbc3ccf1ac95343e897ecffef0a2f42
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92649316"
---
# <a name="custom-host-samples"></a>Примеры пользовательских узлов

В этом разделе содержится пример кода для написания пользовательского узла. С помощью Microsoft Visual Studio можно создать консольное приложение, а затем скопировать код из разделов этого раздела в ведущее приложение.

## <a name="in-this-section"></a>в этом разделе

 [Пример Host01](./host01-sample.md) В этом примере показано, как реализовать ведущее приложение, которое использует базовый пользовательский узел.

 [Пример Host02](./host02-sample.md) В этом примере показано, как создать ведущее приложение, которое использует среду выполнения Windows PowerShell вместе с реализацией пользовательского узла. Ведущее приложение устанавливает немецкий язык и региональные параметры, запускает командлет [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) и отображает результаты, как показано в pwrsh.exe, а затем выводит текущие данные и время на немецком языке.

 [Пример Host03](./host03-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль.

 [Пример Host04](./host04-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль. Это приложение также поддерживает отображение запросов, позволяющих пользователю выбрать несколько вариантов.

 [Пример Host05](./host05-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль. Это ведущее приложение также поддерживает вызовы удаленных компьютеров с помощью командлетов [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) и [Exit-PSSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) .

 [Пример Host06](./host06-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль. Кроме того, в этом примере используются интерфейсы API создателя токенов для указания цвета текста, вводимого пользователем.

## <a name="see-also"></a>См. также
