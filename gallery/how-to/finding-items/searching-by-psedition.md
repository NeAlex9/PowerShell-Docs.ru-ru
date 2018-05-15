---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: Элементы с совместимыми выпусками PowerShell
ms.openlocfilehash: dd2c67417994e960845f7cef09320a0f688a0212
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="items-with-compatible-powershell-editions"></a>Элементы с совместимыми выпусками PowerShell

Начиная с версии 5.1 доступны различные выпуски среды PowerShell, что означает различные наборы возможностей и совместимость с разными платформами.

- **Выпуск Desktop Edition:** построен на основе .NET Framework и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в полноценных выпусках Windows, таких как Server Core и Windows Desktop.
- **Выпуск Core Edition:** построен на основе .NET Core и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в выпусках Windows с ограниченными возможностями, таких как Nano Server и Windows IoT.

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-items-compatible-for-specific-powershell-editions"></a>Коллекция PowerShell извлекает поддерживаемые метаданные PSEditions и позволяет отфильтровывать элементы, совместимые с конкретными выпусками PowerShell

Если элемент имеет указанные совместимые версии PSEdition, они будут перечислены в разделе "Выпуски PowerShell" на странице отображения элемента, а также в результатах элементов.

![Страница отображения элемента с выпусками PSEdition](../../Images/ItemDisplayPageWithPSEditions.PNG)

## <a name="search-for-items-in-the-gallery-ui-which-works-on-powershellcore"></a>Поиск элементов в коллекции пользовательского интерфейса, работающих в PowerShellCore

Для фильтрации элементов в коллекции PowerShell используйте Tags:"PSEdition_Desktop" и Tags:"PSEdition_Core".

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Для поиска элементов, совместимых с выпуском PowerShell Core, используйте Tags:"PSEdition_Core".

![Результаты поиска элементов, совместимых с Core PSEdition](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Для поиска элементов, совместимых с выпуском PowerShell Desktop, используйте Tags:"PSEdition_Desktop".

![Результаты поиска элементов, совместимых с Desktop PSEdition](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-items-with-compatible-powershell-editions"></a>Дополнительные сведения о разработке и поиске элементов с совместимыми выпусками PowerShell

- [Модули с PSEdition](../../concepts/module-psedition-support.md)
- [Скрипты с PSEdition](../../concepts/script-psedition-support.md)