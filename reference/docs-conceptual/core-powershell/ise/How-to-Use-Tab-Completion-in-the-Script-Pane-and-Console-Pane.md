---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Использование заполнения нажатием клавиши TAB в областях сценариев и консоли
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: e1f8146b6113a82fd3d857c98550ec2e459715a4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954931"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a><span data-ttu-id="fa416-103">Использование заполнения нажатием клавиши TAB в областях сценариев и консоли</span><span class="sxs-lookup"><span data-stu-id="fa416-103">How to Use Tab Completion in the Script Pane and Console Pane</span></span>

<span data-ttu-id="fa416-104">Заполнение нажатием клавиши TAB предоставляет автоматическую справку при вводе в области скриптов или команд.</span><span class="sxs-lookup"><span data-stu-id="fa416-104">Tab completion provides automatic help when you are typing in the Script Pane or in the Command Pane.</span></span> <span data-ttu-id="fa416-105">Чтобы воспользоваться этой функцией, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fa416-105">Use the following steps to take advantage of this feature:</span></span>

## <a name="to-automatically-complete-a-command-entry"></a><span data-ttu-id="fa416-106">Автоматическое завершение ввода команды</span><span class="sxs-lookup"><span data-stu-id="fa416-106">To automatically complete a command entry</span></span>

<span data-ttu-id="fa416-107">В области команд или сценариев введите несколько символов команды и нажмите клавишу TAB, чтобы выбрать нужный текст завершения.</span><span class="sxs-lookup"><span data-stu-id="fa416-107">In the Command Pane or Script Pane, type a few characters of a command and then press TAB to select the desired completion text.</span></span> <span data-ttu-id="fa416-108">Если с изначально введенного текста начинается несколько элементов, нажимайте клавишу TAB, пока не появится нужный.</span><span class="sxs-lookup"><span data-stu-id="fa416-108">If multiple items begin with the text that you initially typed, then continue pressing Tab until the item you want appears.</span></span> <span data-ttu-id="fa416-109">Заполнение нажатием клавиши TAB позволяет ввести имя командлета, параметра, переменной, свойства объекта или путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="fa416-109">Tab completion can help with typing a cmdlet name, parameter name, variable name, object property name, or a file path.</span></span>

> [!NOTE]
> <span data-ttu-id="fa416-110">В области сценариев нажатие клавиши TAB автоматически завершает команду только при редактировании файлов PS1, PSD1 или PSM1.</span><span class="sxs-lookup"><span data-stu-id="fa416-110">In the Script Pane, pressing TAB will automatically complete a command only when you are editing .ps1, .psd1, or .psm1 files.</span></span> <span data-ttu-id="fa416-111">Заполнение нажатием клавиши TAB работает в любое время при вводе в области команд.</span><span class="sxs-lookup"><span data-stu-id="fa416-111">Tab completion works any time when you are typing in the Command Pane.</span></span>

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a><span data-ttu-id="fa416-112">Автоматическое завершение ввода для параметра командлета</span><span class="sxs-lookup"><span data-stu-id="fa416-112">To automatically complete a cmdlet parameter entry</span></span>

<span data-ttu-id="fa416-113">В области команд или сценариев введите командлет, поставьте после него дефис и нажмите клавишу TAB.</span><span class="sxs-lookup"><span data-stu-id="fa416-113">In the Command Pane or Script pane, type a cmdlet followed by a dash, and then press TAB.</span></span>

<span data-ttu-id="fa416-114">Например, введите `Get-Process -` и нажмите клавишу TAB несколько раз для отображения параметров командлета по очереди.</span><span class="sxs-lookup"><span data-stu-id="fa416-114">For example, type `Get-Process -` and then press TAB multiple times to display each of the parameters for the cmdlet in turn.</span></span>

## <a name="see-also"></a><span data-ttu-id="fa416-115">См. также</span><span class="sxs-lookup"><span data-stu-id="fa416-115">See Also</span></span>

- [<span data-ttu-id="fa416-116">Введение в интегрированную среду сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa416-116">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="fa416-117">Создание вкладки PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa416-117">How to Create a PowerShell Tab</span></span>](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)