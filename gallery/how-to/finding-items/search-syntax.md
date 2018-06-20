---
ms.date: 06/12/2017
contributor: JKeithB
keywords: коллекции,powershell,командлет,psgallery
title: Синтаксис поиска по коллекции
ms.openlocfilehash: 52fca21a00bcc6e3789bceb331acf5bc771bb0f2
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188417"
---
# <a name="gallery-search-syntax"></a>Синтаксис поиска по коллекции

Коллекция PowerShell содержит текстовое окно поиска, где можно использовать слова, фразы и выражения с ключевыми словами, чтобы сузить результаты поиска.

## <a name="search-by-keywords"></a>Поиск по ключевым словам

    dsc azure sql

Поисковая система пытается показать соответствующие документы, содержащие все три ключевые слова.

## <a name="search-using-phrases-and-keywords"></a>Поиск с использованием ключевых слов и фраз

    "azure sql" deployment

При вводе фразы, заключенной в кавычки (""), выполняется поиск конкретной фразы, а не отдельных ключевых слов.
Соответствующие документы обычно содержат точную фразу azure sql, включая варианты (с другим регистром букв, например Azure SQL), а также обычно содержат слово "развертывание".

## <a name="filtering-on-fields"></a>Фильтрация по полям

Вы можете выполнять поиск конкретного идентификатора элемента (ID, Id или id) или других полей, указывая перед условиями поиска имя поля.

В настоящее время для поиска доступны следующие поля: Id, Version, Tags, Author, Owner, Functions, Cmdlets, DscResources и PowerShellVersion.

[В чем отличие между идентификатором и заголовком? Идентификатор — это имя, используемое в консоли. Заголовок — это то, что отображается в верхней части страницы элемента в результатах поиска.]

## <a name="examples"></a>Примеры

    ID:"PSReadline"
    id:"AzureRM.Profile"

— поиск элементов со словами PSReadline или AzureRM.Profile в поле ID;

    Id:"AzureRM.Profile"

— еще один способ поиска элементов со словом AzureRM.Profile в поле ID.

Фильтр Id — это сопоставление вложенных строк, поэтому при следующем поиске:

    Id:"azure"

вы получите такие результаты, как AzureRM.Profile и Azure.Storage;

можно также выполнить поиск с несколькими ключевыми словами в одном поле; вы также можете сочетать разные поля.

    id:azure tags:intellisense
    id:azure id:storage

Можно выполнять поиск следующих фраз.

    id:"azure.storage"


Чтобы найти все элементы с тегом DSC:

    Tags:"DSC"

Чтобы найти все элементы с указанной функцией:

    Functions:"Update-AzureRM"

Чтобы найти все элементы с указанным командлетом:

    Cmdlets:"Get-AzureRmEnvironment"

Чтобы найти все элементы с указанным именем ресурса DSC:

    DscResources:"xArchive"

Чтобы найти все элементы с указанной версией PowerShellVersion:

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


Наконец, если вы используете поле, которое не поддерживается, например commands, мы просто проигнорируем его и выполним поиск по всем полям. Поэтому следующий запрос

    commands:blobs storage

интерпретируется точно так же, как этот запрос:

    blobs storage