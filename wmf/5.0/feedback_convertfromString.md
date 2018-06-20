---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: e4588e8c69efb965cd33c273ad09a8bef8e9bf16
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189573"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a>Извлечение и анализ структурированных объектов вне строки
Здесь также расширена функциональность командлета ConvertFrom-String:

-   Удалено свойство текста экстента по умолчанию. Теперь его можно включить с помощью параметра -IncludeExtent.

-   Исправлены многие ошибки в алгоритмах обучения благодаря отзывам MVP и участников сообщества.

-   Новый параметр -UpdateTemplate для сохранения результатов алгоритма обучения в комментарий внутри файла шаблона. Это делает затраты на процесс обучения (являющийся самым медленным этапом) единовременными. Выполнение Convert-String с шаблоном, содержащим закодированный обучающий алгоритм, теперь осуществляется практически мгновенно.


<a name="extract-and-parse-structured-objects-out-of-string-content"></a>Извлечение и анализ структурированных объектов вне строки
----------------------------------------------------------

При сотрудничестве с [Microsoft Research](http://research.microsoft.com/) был добавлен новый командлет **ConvertFrom-String**.

Он поддерживает два режима: базовый анализ с разделением и анализ с управлением автоматически создаваемым примером.

Анализ с разделением, используемый по умолчанию, разбивает входные данные с помощью пробелов и присваивает имена свойств получаемым группам. Разделитель можно настроить:

> 1 \[C:\\temp\].&gt;&gt; "Hello World" | ConvertFrom-String | Format-Table -Auto

P1    P2
--    --

Командлет также поддерживает анализ с управлением автоматически создаваемым примером, основанные на исследованиях технологии [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) в [Microsoft Research](http://research.microsoft.com).

Для начала рассмотрим текстовую адресную книгу:

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

    Thomas Hardy

    Seattle, WA

    Christina Berglund

    Redmond, WA

    Hanna Moos

    Puyallup, WA

Скопируйте несколько примеров в файл, который будет использоваться в качестве шаблона:

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA



Заключите извлекаемые данные в фигурные скобки, при этом им присваивается имя. Поскольку свойство **Name** (и другие связанные с ним свойства) могут встречаться несколько раз, используйте звездочку (\*), чтобы указать, что результат представлен несколькими записями (вместо извлечения множества свойств в одну запись):

    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}

Используя этот набор примеров, **ConvertFrom-String** может автоматически извлекать выходные данные на основе объектов из входных файлов с аналогичной структурой.

> 2 \[C:\\temp\]
>
> &gt;&gt; Get-Content .\\addresses.output.txt | ConvertFrom-String -TemplateFile .\\addresses.template.txt | &gt;&gt;&gt; Format-Table -Auto
>
> ExtentText                     Name               City     State
> ----------                     ----               ----     -----
> Ana Trujillo...                Ana Trujillo       Redmond  WA Antonio Moreno...              Antonio Moreno     Renton   WA Thomas Hardy...                Thomas Hardy       Seattle  WA Christina Berglund...          Christina Berglund Redmond  WA Hanna Moos...                  Hanna Moos         Puyallup WA

В целях дополнительной обработки извлеченного текста свойство **ExtentText** может фиксировать необработанный текст, из которого извлекалась запись. Чтобы дать отзыв об этой функции или предоставить содержимое, для которого у вас не получается составить примеры, отправьте сообщение электронной почты на адрес <psdmfb@microsoft.com>.
