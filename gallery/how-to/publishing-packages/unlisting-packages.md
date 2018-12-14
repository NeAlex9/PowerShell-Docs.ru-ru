---
ms.date: 06/12/2017
contributor: JKeithB
keywords: коллекции,powershell,командлет,psgallery
title: Исключение пакетов
ms.openlocfilehash: fb66fd23dae1d4640056a764c31426f61f56d910
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50003912"
---
# <a name="unlisting-packages"></a>Исключение пакетов

**Почему в программе нет команды, позволяющей удалить пакет из коллекции PowerShell?**

Коллекция PowerShell не позволяет пользователям полностью удалять пакеты.
Это позволяет другим разработчикам использовать зависимости с вашими пакетами и не беспокоиться об их нарушении в будущем.
Например, если модуль Pester зависит от модуля Azure и этот модуль удаляется из коллекции, пользователь больше не сможет использовать модуль Pester.

Вместо того, чтобы удалять пакет, его можно исключить.

**Что происходит при исключении пакета из коллекции PowerShell?**

Пакет, исключенный из числа модулей или скриптов в коллекции PowerShell, будет удален из вкладки "Пакеты". Кроме того, исключенные пакеты не отображаются в результатах поиска.
Единственный способ загрузить исключенный пакет — это точно указать его имя и версию.
Таким образом, исключение пакета не нарушает работу других модулей или скриптов, которые от него зависят.

Чтобы исключить пакет, откройте страницу сведений о пакете и выберите "Удалить модуль". Снимите флажок "В списке" и нажмите кнопку "Сохранить".

**Как удалить пакет?**

В ситуации, когда пакет необходимо удалить, обратитесь к администраторам коллекции PowerShell.
Удаление элементов будет оправдано в следующих случаях:
- Проблемы с нарушением авторских прав.
- Пакет содержит потенциально вредоносное содержимое.
- Пакет содержит конфиденциальные данные.

Чтобы отправить запрос об удалении пакета администраторам коллекции PowerShell, откройте страницу сведений о пакете и выберите "Обратиться в службу поддержки".