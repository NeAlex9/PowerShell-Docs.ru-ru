---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: e2c9233734a6ede04e8ec2bbad05950cbb31cbba
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057516"
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="0bc5a-102">Поддержка модулей для объявления диапазонов версий (1.\* и т. д.)</span><span class="sxs-lookup"><span data-stu-id="0bc5a-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="0bc5a-103">В сочетании с **-MinimumVersion** **-MaximumVersion** дает пользователю возможность получения и импорта модуля в пределах определенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="0bc5a-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="0bc5a-104">Параметр также поддерживает **.**\*.</span><span class="sxs-lookup"><span data-stu-id="0bc5a-104">The parameter also support **.**\*.</span></span> <span data-ttu-id="0bc5a-105">В следующем примере показано, как это работает:</span><span class="sxs-lookup"><span data-stu-id="0bc5a-105">The following example shows how it works:</span></span>

<span data-ttu-id="0bc5a-106">Теперь вы можете сочетать **-MinimumVersion** и **-MaximumVersion**, чтобы импортировать модуль из определенного диапазона:</span><span class="sxs-lookup"><span data-stu-id="0bc5a-106">Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:</span></span>

```powershell
PS C:\> Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*

VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```
