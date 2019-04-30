---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Прямой вызов методов ресурсов DSC
ms.openlocfilehash: cf237f638593706e5959e2bcc0d851b0e55baf0e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079631"
---
# <a name="calling-dsc-resource-methods-directly"></a>Прямой вызов методов ресурсов DSC

>Область применения. Windows PowerShell 5.0

Командлет [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) можно использовать для прямого вызова функций или методов ресурса DSC (функций **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource** ресурса на основе MOF-файла или методов **Get**, **Set** и **Test** ресурса на основе класса).
Этот командлет могут использовать сторонние разработчики, которым требуется использовать ресурсы DSC, кроме того, он удобен для разработки ресурсов.

Командлет обычно используется в сочетании со свойством метаконфигурации `refreshMode = 'Disabled'`, однако он доступен независимо от значения **refreshMode**.

При вызове командлета **Invoke-DscResource** указать, какой метод или функцию необходимо вызвать, можно с помощью параметра **Method**. Свойства ресурса указываются путем передачи хэш-таблицы в качестве значения параметра **Property**.

Ниже приведены примеры прямого вызова методов ресурсов:

## <a name="ensure-a-file-is-present"></a>Проверка наличия файла

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Тестирование наличия файла

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>Получение содержимого файла

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Примечание**. Прямой вызов методов составного ресурса не поддерживается. Вместо этого вызывайте методы базовых ресурсов, входящих в составной ресурс.

## <a name="see-also"></a>См. также
- [Написание пользовательских ресурсов DSC с использованием MOF](../resources/authoringResourceMOF.md)
- [Написание пользовательских ресурсов DSC с использованием классов PowerShell](../resources/authoringResourceClass.md)
- [Отладка ресурсов DSC](../troubleshooting/debugResource.md)