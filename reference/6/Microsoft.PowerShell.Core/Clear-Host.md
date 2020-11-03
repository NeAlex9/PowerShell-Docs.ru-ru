---
external help file: System.Management.Automation.dll-Help.xml
keywords: powershell,командлет
Locale: en-US
Module Name: ''
ms.date: 06/09/2017
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/clear-host?view=powershell-6&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Clear-Host;
ms.openlocfilehash: 4c0732a8d1e40cdc584839db62f61a4e9f7b618c
ms.sourcegitcommit: 2e497178126b2b33a169ff04c31e251e0b59e89b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2020
ms.locfileid: "93209121"
---
# <span data-ttu-id="759c5-103">Clear-Host;</span><span class="sxs-lookup"><span data-stu-id="759c5-103">Clear-Host</span></span>

## <span data-ttu-id="759c5-104">Краткий обзор</span><span class="sxs-lookup"><span data-stu-id="759c5-104">SYNOPSIS</span></span>

<span data-ttu-id="759c5-105">Удаляет отображаемые данные в основной программе.</span><span class="sxs-lookup"><span data-stu-id="759c5-105">Clears the display in the host program.</span></span>

## <span data-ttu-id="759c5-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="759c5-106">SYNTAX</span></span>

```
Clear-Host [<CommonParameters>]
```

## <span data-ttu-id="759c5-107">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="759c5-107">DESCRIPTION</span></span>

<span data-ttu-id="759c5-108">`Clear-Host`Функция удаляет весь текст из текущего экрана, включая команды и выходные данные, которые могли накапливаться.</span><span class="sxs-lookup"><span data-stu-id="759c5-108">The `Clear-Host` function removes all text from the current display, including commands and output that might have accumulated.</span></span> <span data-ttu-id="759c5-109">При выполнении этой команды отобразится командная строка.</span><span class="sxs-lookup"><span data-stu-id="759c5-109">When complete, it displays the command prompt.</span></span> <span data-ttu-id="759c5-110">Можно использовать имя функции или ее псевдоним, `cls` .</span><span class="sxs-lookup"><span data-stu-id="759c5-110">You can use the function name or its alias, `cls`.</span></span>

<span data-ttu-id="759c5-111">`Clear-Host` влияет только на текущее отображение.</span><span class="sxs-lookup"><span data-stu-id="759c5-111">`Clear-Host` affects only the current display.</span></span> <span data-ttu-id="759c5-112">Эта команда не удаляет сохраненные результаты или какие-либо элементы сеанса.</span><span class="sxs-lookup"><span data-stu-id="759c5-112">It does not delete saved results or remove any items from the session.</span></span> <span data-ttu-id="759c5-113">Эта функция не затрагивает специфические для сеанса элементы, такие как переменные или функции.</span><span class="sxs-lookup"><span data-stu-id="759c5-113">Session-specific items, such as variables and functions, are not affected by this function.</span></span>

<span data-ttu-id="759c5-114">Поскольку поведение `Clear-Host` функции определяется ведущим приложением, `Clear-Host` может работать по-разному в различных ведущих программах.</span><span class="sxs-lookup"><span data-stu-id="759c5-114">Because the behavior of the `Clear-Host` function is determined by the host program, `Clear-Host` might work differently in different host programs.</span></span>

## <span data-ttu-id="759c5-115">Примеры</span><span class="sxs-lookup"><span data-stu-id="759c5-115">EXAMPLES</span></span>

### <span data-ttu-id="759c5-116">Пример 1</span><span class="sxs-lookup"><span data-stu-id="759c5-116">Example 1</span></span>

```
# Before

PS C:\> Get-Process

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    843      33    14428      22556    99    17.41   1688 CcmExec
     44       6     2196       4964    52     0.23    692 conhost
    646      12     2332       4896    49     1.12    388 csrss
    189      11     2860       7084   114     0.66   2896 csrss
     78      11     1876       4008    42     0.22   4000 csrss
     76       7     1848       5064    54     0.08   1028 dwm
    610      41    23952      44048   208     4.40   2080 explorer
      0       0        0         24     0               0 Idle
    182      32     7692      15980    91     0.23   3056 LogonUI
    186      25     7832      16068    91     0.27   3996 LogonUI
   1272      32    11512      20432    58    25.07    548 lsass
    267      10     3536       6736    34     0.80    556 lsm
    137      17     3520       7472    61     0.05   1220 msdtc
    447      31    70316      84476   201 1,429.67    836 MsMpEng
    265      18     7136      15628   134     2.20   3544 msseces
    248      16     6476       4076    76     0.22   1592 NisSrv
    368      25    61312      65508   614     1.78    848 powershell
    101       8     2304       6624    70     0.64   3648 rdpclip
    258      15     6804      12156    50     2.65    536 services
...

PS C:\> cls
#After

PS C:>
```

<span data-ttu-id="759c5-117">Эта команда использует `cls` псевдоним `Clear-Host` для очистки текущего экрана.</span><span class="sxs-lookup"><span data-stu-id="759c5-117">This command uses the `cls` alias of `Clear-Host` to clear the current display.</span></span>

## <span data-ttu-id="759c5-118">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="759c5-118">PARAMETERS</span></span>

### <span data-ttu-id="759c5-119">Общие параметры</span><span class="sxs-lookup"><span data-stu-id="759c5-119">CommonParameters</span></span>
<span data-ttu-id="759c5-120">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="759c5-120">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="759c5-121">См. сведения в разделе [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="759c5-121">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="759c5-122">Входные данные</span><span class="sxs-lookup"><span data-stu-id="759c5-122">INPUTS</span></span>

### <span data-ttu-id="759c5-123">Нет</span><span class="sxs-lookup"><span data-stu-id="759c5-123">None</span></span>

<span data-ttu-id="759c5-124">Вы не можете передать входные данные в `Clear-Host` .</span><span class="sxs-lookup"><span data-stu-id="759c5-124">You cannot pipe input to `Clear-Host`.</span></span>

## <span data-ttu-id="759c5-125">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="759c5-125">OUTPUTS</span></span>

### <span data-ttu-id="759c5-126">Нет</span><span class="sxs-lookup"><span data-stu-id="759c5-126">None</span></span>

<span data-ttu-id="759c5-127">`Clear-Host` не создает никаких выходных данных</span><span class="sxs-lookup"><span data-stu-id="759c5-127">`Clear-Host` does not generate any output</span></span>

## <span data-ttu-id="759c5-128">ПРИМЕЧАНИЯ</span><span class="sxs-lookup"><span data-stu-id="759c5-128">NOTES</span></span>

<span data-ttu-id="759c5-129">`Clear-Host` — Это простая функция, а не расширенная функция.</span><span class="sxs-lookup"><span data-stu-id="759c5-129">`Clear-Host` is a simple function, not an advanced function.</span></span> <span data-ttu-id="759c5-130">Таким образом, в команде нельзя использовать общие параметры, такие как **Debug** `Clear-Host` .</span><span class="sxs-lookup"><span data-stu-id="759c5-130">As such, you cannot use common parameters, such as **Debug** , in a `Clear-Host` command.</span></span>

## <span data-ttu-id="759c5-131">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="759c5-131">RELATED LINKS</span></span>

[<span data-ttu-id="759c5-132">Get-Host</span><span class="sxs-lookup"><span data-stu-id="759c5-132">Get-Host</span></span>](../Microsoft.PowerShell.Utility/Get-Host.md)

[<span data-ttu-id="759c5-133">Out-Host</span><span class="sxs-lookup"><span data-stu-id="759c5-133">Out-Host</span></span>](Out-Host.md)

[<span data-ttu-id="759c5-134">Read-Host</span><span class="sxs-lookup"><span data-stu-id="759c5-134">Read-Host</span></span>](../Microsoft.PowerShell.Utility/Read-Host.md)

[<span data-ttu-id="759c5-135">Write-Host</span><span class="sxs-lookup"><span data-stu-id="759c5-135">Write-Host</span></span>](../Microsoft.PowerShell.Utility/Write-Host.md)
