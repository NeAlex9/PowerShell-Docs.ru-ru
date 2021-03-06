---
title: Рассмотрение сообщений о проблемах
description: Эта статья описывает работу с проблемами в команде специалистов по PowerShell-Docs.
ms.date: 12/09/2020
ms.topic: conceptual
ms.openlocfilehash: 72267137a2657f51e5f616113adf92d80647acad
ms.sourcegitcommit: 61765d08321623743dc5db5367160f6982fe7857
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2020
ms.locfileid: "99601076"
---
# <a name="how-we-manage-issues"></a>Рассмотрение сообщений о проблемах

В этой статье описывается, как мы управляем проблемами в репозитории PowerShell-Docs. Изначально это памятка для участников команды PowerShell-Docs. Он опубликован здесь, чтобы обеспечить прозрачность процесса для наших общедоступных участников.

## <a name="sources-of-issues"></a>Источники проблем

- Участники из сообщества
- Внутренние участники
- Расшифровка комментариев из каналов социальных сетей
- Комментарии, полученные через форму отзыва в документации

## <a name="response-time-targets"></a>Целевые показатели времени отклика

80% новых проблем закрываются в течение 3 рабочих дней.

- Рассмотрено — 1 рабочие дни
- Исправление или изменение — 10 рабочих дней

### <a name="labeling--milestones"></a>Метки и вехи

#### <a name="label-types"></a>Типы меток

|   Тип   | Описание                                                         |
| -------- | ------------------------------------------------------------------- |
| Область     | Используется для указания того, к какой части PowerShell или документации относится проблема.<br>Позволяет разработчикам функций легко находить проблемы, связанные с их функциями. |
| Проблема    | Указывает тип проблемы                                         |
| Приоритет | Указывает приоритет проблемы. Диапазон значений 0 (высокий) — 4 (низкий)  |
| Состояние   | Указывает состояние рабочего элемента или причины его закрытия          |
| Тег      | Метки, используемые для дополнительной классификации                        |
| Ожидание  | Указывает, что мы ожидаем какого-либо другого события         |

#### <a name="milestones"></a>Вехи

Проблемы и запросы на вытягивание должны помечаться соответствующими вехами. Если проблема не относится к определенной версии, то веха не используется. Вытягивание и связанные с ним проблемы с изменениями, которые еще необходимо объединить в базу кода PowerShell, должны быть назначены **будущей** вехе. После слияния изменения кода измените веху на соответствующую версию.

|    Веха     |                    Описание                     |
| ---------------- | -------------------------------------------------- |
| 7.0.0            | Рабочие элементы, связанные с PowerShell 7.0               |
| 7.1.0            | Рабочие элементы, связанные с PowerShell 7.1               |
| 7.2.0            | Рабочие элементы, связанные с PowerShell 7,2               |
| Планируется реализация.           | Рабочие элементы, связанные с будущей версией PowerShell          |

## <a name="triage-process"></a>Процесс рассмотрения

Участники группы документации PowerShell могут просматривать проблемы ежедневно и рассматривать новые проблемы по мере их поступления. Команда отвечает еженедельно, чтобы обсудить проблемы, которые требуют рассмотрения или остаются нерешенными.

### <a name="misplaced-product-feedback"></a>Ошибочно адресованный отзыв о продукте

- Введите комментарий, перенаправляющий клиента на правильный канал обратной связи.
- Необязательное действие: Скопируйте проблему в соответствующий канал обратной связи, добавьте ссылку на скопированный элемент и закройте проблему. НЕ копируйте проблемы в UserVoice.

  По умолчанию для проблем с PowerShell используется расположение [https://github.com/PowerShell/PowerShell/issues/new/choose](https://github.com/PowerShell/PowerShell/issues/new/choose) .

  Следующие предметные области имеют различные расположения для проблем:

  | Субъекты |                                                     URL-адрес для отзыва о продукте                                                     |
  | -------- | ---------------------------------------------------------------------------------------------------------------------------- |
  | DSC      | [https://windowsserver.uservoice.com/forums/301869-powershell](https://windowsserver.uservoice.com/forums/301869-powershell) |
  | gallery  | [https://github.com/powershell/powershellgallery/issues/new](https://github.com/powershell/powershellgallery/issues/new)     |
  | jea      | [https://github.com/powershell/jea/issues/new](https://github.com/powershell/jea/issues/new)                                 |
  | wmf      | [https://windowsserver.uservoice.com/forums/301869-powershell](https://windowsserver.uservoice.com/forums/301869-powershell) |

### <a name="support-requests"></a>Запросы в службу поддержки

- Если вопрос в службу поддержки прост, ответьте на него и закройте проблему.
- Если вопрос сложный или отправитель задает дополнительные вопросы, перенаправьте его на форумы и в каналы поддержки. Вариант текста для перенаправления на форумы:

  ```Markdown
  > This is not the right forum for these kinds of questions. Try posting your question in a
  > community support forum. For a list of community forums see:
  > https://docs.microsoft.com/powershell/scripting/community/community-support
  ```

### <a name="code-of-conduct-violations"></a>Нарушение кодекса поведения

- При необходимости отредактируйте проблему, чтобы удалить оскорбительное содержимое.
- Введите комментарий о том, что проблема является спамом, закройте проблему и заблокируйте ее, чтобы запретить добавление комментариев.
- Каждое нарушение следует обсудить при еженедельном рассмотрении, чтобы определить потребность в дальнейших действиях (отчет для GitHub или Microsoft Legal).
