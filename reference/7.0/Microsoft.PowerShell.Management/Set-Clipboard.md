---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 12/03/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.management/set-clipboard?view=powershell-7&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Set-Clipboard
ms.openlocfilehash: efb24b14122ad37043636d999afaa4199eb3097b
ms.sourcegitcommit: 7b376314e7640c39a53aac9f0db8bb935514a960
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2020
ms.locfileid: "96564379"
---
# <span data-ttu-id="3a92e-102">Set-Clipboard</span><span class="sxs-lookup"><span data-stu-id="3a92e-102">Set-Clipboard</span></span>

## <span data-ttu-id="3a92e-103">Краткий обзор</span><span class="sxs-lookup"><span data-stu-id="3a92e-103">SYNOPSIS</span></span>
<span data-ttu-id="3a92e-104">Задает содержимое буфера обмена.</span><span class="sxs-lookup"><span data-stu-id="3a92e-104">Sets the contents of the clipboard.</span></span>

## <span data-ttu-id="3a92e-105">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="3a92e-105">SYNTAX</span></span>

```
Set-Clipboard [-Value] <string[]> [-Append] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## <span data-ttu-id="3a92e-106">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="3a92e-106">DESCRIPTION</span></span>

<span data-ttu-id="3a92e-107">`Set-Clipboard`Командлет задает содержимое буфера обмена.</span><span class="sxs-lookup"><span data-stu-id="3a92e-107">The `Set-Clipboard` cmdlet sets the contents of the clipboard.</span></span>

> [!NOTE]
> <span data-ttu-id="3a92e-108">В Linux для этого командлета требуется, `xclip` чтобы программа была в пути.</span><span class="sxs-lookup"><span data-stu-id="3a92e-108">On Linux, this cmdlet requires the `xclip` utility to be in the path.</span></span>

## <span data-ttu-id="3a92e-109">Примеры</span><span class="sxs-lookup"><span data-stu-id="3a92e-109">EXAMPLES</span></span>

### <span data-ttu-id="3a92e-110">Пример 1. копирование текста в буфер обмена</span><span class="sxs-lookup"><span data-stu-id="3a92e-110">Example 1: Copy text to the clipboard</span></span>

```powershell
Set-Clipboard -Value "This is a test string"
```

### <span data-ttu-id="3a92e-111">Пример 2. копирование содержимого файла в буфер обмена</span><span class="sxs-lookup"><span data-stu-id="3a92e-111">Example 2: Copy the contents of a file to the clipboard</span></span>

<span data-ttu-id="3a92e-112">В этом примере содержимое файла переводится в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="3a92e-112">This example pipes the contents of a file to the clipboard.</span></span> <span data-ttu-id="3a92e-113">В этом примере мы получаем открытый ключ SSH, чтобы его можно было вставлять в другое приложение, например GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a92e-113">In this example, we are getting a public ssh key so that it can be pasted into another application, like GitHub.</span></span>

```powershell
Get-Content C:\Users\user1\.ssh\id_ed25519.pub | Set-Clipboard
```

## <span data-ttu-id="3a92e-114">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="3a92e-114">PARAMETERS</span></span>

### <span data-ttu-id="3a92e-115">— Добавление</span><span class="sxs-lookup"><span data-stu-id="3a92e-115">-Append</span></span>

<span data-ttu-id="3a92e-116">Указывает, что командлет не очищает буфер обмена и добавляет к нему содержимое.</span><span class="sxs-lookup"><span data-stu-id="3a92e-116">Indicates that the cmdlet does not clear the clipboard and appends content to it.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="3a92e-117">-Confirm</span><span class="sxs-lookup"><span data-stu-id="3a92e-117">-Confirm</span></span>

<span data-ttu-id="3a92e-118">Запрос подтверждения перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="3a92e-118">Prompts you for confirmation before running the cmdlet.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="3a92e-119">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="3a92e-119">-WhatIf</span></span>

<span data-ttu-id="3a92e-120">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="3a92e-120">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="3a92e-121">Командлет не выполняется.</span><span class="sxs-lookup"><span data-stu-id="3a92e-121">The cmdlet is not run.</span></span>

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="3a92e-122">-Value</span><span class="sxs-lookup"><span data-stu-id="3a92e-122">-Value</span></span>

<span data-ttu-id="3a92e-123">Строковые значения, которые необходимо добавить в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="3a92e-123">The string values to be added to the clipboard.</span></span>

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### <span data-ttu-id="3a92e-124">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="3a92e-124">CommonParameters</span></span>

<span data-ttu-id="3a92e-125">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3a92e-125">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="3a92e-126">См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="3a92e-126">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="3a92e-127">Входные данные</span><span class="sxs-lookup"><span data-stu-id="3a92e-127">INPUTS</span></span>

### <span data-ttu-id="3a92e-128">System.String[]</span><span class="sxs-lookup"><span data-stu-id="3a92e-128">System.String[]</span></span>

## <span data-ttu-id="3a92e-129">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="3a92e-129">OUTPUTS</span></span>

## <span data-ttu-id="3a92e-130">ПРИМЕЧАНИЯ</span><span class="sxs-lookup"><span data-stu-id="3a92e-130">NOTES</span></span>

<span data-ttu-id="3a92e-131">В редких случаях при `Set-Clipboard` быстром выполнении с большим количеством значений, например в цикле, вы можете регулярно получать пустое значение из буфера обмена.</span><span class="sxs-lookup"><span data-stu-id="3a92e-131">In rare cases when using `Set-Clipboard` with a high number of values in rapid succession, like in a loop, you might sporadically get a blank value from the clipboard.</span></span> <span data-ttu-id="3a92e-132">Это можно исправить с помощью `Start-Sleep -Milliseconds 1` в цикле.</span><span class="sxs-lookup"><span data-stu-id="3a92e-132">This can be fixed by using `Start-Sleep -Milliseconds 1` in the loop.</span></span>

## <span data-ttu-id="3a92e-133">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="3a92e-133">RELATED LINKS</span></span>

[<span data-ttu-id="3a92e-134">Get-Clipboard</span><span class="sxs-lookup"><span data-stu-id="3a92e-134">Get-Clipboard</span></span>](Get-Clipboard.md)
