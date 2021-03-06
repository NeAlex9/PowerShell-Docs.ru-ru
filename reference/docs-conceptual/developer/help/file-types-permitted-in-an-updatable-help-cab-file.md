---
ms.date: 03/22/2012
ms.topic: reference
title: Типы файлов, которые могут использоваться в CAB-файле обновляемой справки
description: Типы файлов, которые могут использоваться в CAB-файле обновляемой справки
ms.openlocfilehash: bb69b8b89a9a3a5c8c00059ec404a4d41a5db9a5
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92654738"
---
# <a name="file-types-permitted-in-an-updatable-help-cab-file"></a>Типы файлов, которые могут использоваться в CAB-файле обновляемой справки

Несжатое содержимое CAB-файла по умолчанию ограничено 1 ГБ. Чтобы обойти это ограничение, пользователям необходимо использовать параметр **Force** командлетов [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) и [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) .

Для обеспечения безопасности файлов справки, загружаемых из Интернета, обновляемый CAB-файл справки может включать только перечисленные ниже типы файлов. Командлет [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) проверяет все файлы по схемам разделов справки. Если `Update-Help` командлет встречает файл, который является недопустимым или не является разрешенным типом, он не устанавливает недопустимый файл и прекращает установку файлов из CAB-файла на компьютере пользователя.

- Разделы справки на основе XML для командлетов.
- Разделы справки на основе XML для скриптов и функций.
- Разделы справки на основе XML для поставщиков PowerShell.
- Разделы справки на основе текста, например о разделах.

[Обновление — Справка](/powershell/module/Microsoft.PowerShell.Core/Update-Help) проверяет содержимое CAB-файла при его распаковке. Если `Update-Help` находит несовместимые типы файлов в обновляемом CAB-файле справки, он создает завершающую ошибку и останавливает операцию. Он не устанавливает файлы справки из CAB-файла, даже для соответствующих типов файлов.
