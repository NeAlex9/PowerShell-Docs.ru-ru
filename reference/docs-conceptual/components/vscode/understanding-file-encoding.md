---
title: Основные сведения о кодировке файлов в VSCode и PowerShell
description: Настройка кодировки файлов в VSCode и PowerShell
ms.date: 02/28/2019
ms.openlocfilehash: 3283e1262c8eb26906429ecf195cfa0b122b330f
ms.sourcegitcommit: a6e54a305fdeb6482321c77da8066d2f991c93e1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2019
ms.locfileid: "74117412"
---
# <a name="understanding-file-encoding-in-vscode-and-powershell"></a><span data-ttu-id="a9c4d-103">Основные сведения о кодировке файлов в VSCode и PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9c4d-103">Understanding file encoding in VSCode and PowerShell</span></span>

<span data-ttu-id="a9c4d-104">При использовании VS Code для создания и редактирования сценариев PowerShell очень важно, чтобы ваши файлы сохранялись в правильной кодировке символов.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-104">When using VS Code to create and edit PowerShell scripts, it is important that your files are saved using the correct character encoding format.</span></span>

## <a name="what-is-file-encoding-and-why-is-it-important"></a><span data-ttu-id="a9c4d-105">Что такое кодировка и почему она важна?</span><span class="sxs-lookup"><span data-stu-id="a9c4d-105">What is file encoding and why is it important?</span></span>

<span data-ttu-id="a9c4d-106">VSCode управляет интерфейсом между человеком, вводящим строки символов в буфер, и чтением-записью блоков байтов в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-106">VSCode manages the interface between a human entering strings of characters into a buffer and reading/writing blocks of bytes to the filesystem.</span></span> <span data-ttu-id="a9c4d-107">При сохранении файла в VS Code используется кодирование текста для определения того, какие байты получит каждый символ.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-107">When VSCode saves a file, it uses a text encoding to decide what bytes each character becomes.</span></span>

<span data-ttu-id="a9c4d-108">Аналогичным образом, когда оболочка PowerShell запускает скрипт, ей необходимо преобразовать байты из файла в символы для преобразования файла в программу PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-108">Similarly, when PowerShell runs a script it must convert the bytes in a file to characters to reconstruct the file into a PowerShell program.</span></span> <span data-ttu-id="a9c4d-109">Поскольку VSCode записывает файл, а PowerShell считывает файл, им необходимо использовать одну и ту же систему кодировки.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-109">Since VSCode writes the file and PowerShell reads the file, they need to use the same encoding system.</span></span> <span data-ttu-id="a9c4d-110">Этот процесс синтаксического анализа скрипта PowerShell идет так: *байты* -> *символы* -> *лексемы* ->  *дерево абстрактного синтаксиса* -> *выполнение*.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-110">This process of parsing a PowerShell script goes: *bytes* -> *characters* -> *tokens* -> *abstract syntax tree* -> *execution*.</span></span>

<span data-ttu-id="a9c4d-111">И VSCode, и PowerShell устанавливаются с подходящей конфигурацией кодировки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-111">Both VSCode and PowerShell are installed with a sensible default encoding configuration.</span></span> <span data-ttu-id="a9c4d-112">Тем не менее кодировка по умолчанию, используемая PowerShell, была изменена с выпуском PowerShell Core (версии 6.x).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-112">However, the default encoding used by PowerShell has changed with the release of PowerShell Core (v6.x).</span></span> <span data-ttu-id="a9c4d-113">Чтобы избежать проблем с PowerShell или расширениями PowerShell в VSCode, необходимо настроить параметры VSCode и PowerShell должным образом.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-113">To ensure you have no problems using PowerShell or the PowerShell extension in VSCode, you need to configure your VSCode and PowerShell settings properly.</span></span>

## <a name="common-causes-of-encoding-issues"></a><span data-ttu-id="a9c4d-114">Распространенные причины проблемы с кодировкой</span><span class="sxs-lookup"><span data-stu-id="a9c4d-114">Common causes of encoding issues</span></span>

<span data-ttu-id="a9c4d-115">Проблемы с кодировкой возникают, если кодировка VSCode в целом или вашего файла скрипта не совпадает с ожидаемой кодировкой PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-115">Encoding problems occur when the encoding of VSCode or your script file does not match the expected encoding of PowerShell.</span></span> <span data-ttu-id="a9c4d-116">В PowerShell нет способа автоматически определить кодировку файла.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-116">There is no way for PowerShell to automatically determine the file encoding.</span></span>

<span data-ttu-id="a9c4d-117">Проблемы с кодировкой более вероятны при использовании символов не из [7-разрядной кодировки ASCII](https://ascii.cl/).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-117">You're more likely to have encoding problems when you're using characters not in the [7-bit ASCII character set](https://ascii.cl/).</span></span> <span data-ttu-id="a9c4d-118">Например:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-118">For example:</span></span>

- <span data-ttu-id="a9c4d-119">Расширенные небуквенные символы, такие как длинное тире (`—`), неразрывный пробел (` `) или левая двойная кавычка (`“`).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-119">Extended non-letter characters like em-dash (`—`), non-breaking space (` `) or left double quotation mark (`“`)</span></span>
- <span data-ttu-id="a9c4d-120">Латинские символы с диакритикой (`É`, `ü`)</span><span class="sxs-lookup"><span data-stu-id="a9c4d-120">Accented latin characters (`É`, `ü`)</span></span>
- <span data-ttu-id="a9c4d-121">Нелатинские символы, такие как кириллица (`Д`, `Ц`)</span><span class="sxs-lookup"><span data-stu-id="a9c4d-121">Non-latin characters like Cyrillic (`Д`, `Ц`)</span></span>
- <span data-ttu-id="a9c4d-122">Символы иероглифического письма (`本`, `화`, `が`).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-122">CJK characters (`本`, `화`, `が`)</span></span>

<span data-ttu-id="a9c4d-123">Распространенные причины проблем с кодировкой:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-123">Common reasons for encoding issues are:</span></span>

- <span data-ttu-id="a9c4d-124">Настройки кодировок по умолчанию VSCode и PowerShell не были изменены.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-124">The encodings of VSCode and PowerShell have not been changed from their defaults.</span></span> <span data-ttu-id="a9c4d-125">В PowerShell 5.1 и ниже кодировка по умолчанию отличается от используемой в VSCode.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-125">For PowerShell 5.1 and below, the default encoding is different from VSCode's.</span></span>
- <span data-ttu-id="a9c4d-126">Открыт другой редактор, и файл перезаписан в новой кодировке.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-126">Another editor has opened and overwritten the file in a new encoding.</span></span> <span data-ttu-id="a9c4d-127">Это часто происходит с интегрированной средой сценариев.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-127">This often happens with the ISE.</span></span>
- <span data-ttu-id="a9c4d-128">Файл возвращается в систему управления версиями в кодировке, отличной от той, что ожидает VSCode или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-128">The file is checked into source control in an encoding that is different from what VSCode or PowerShell expects.</span></span> <span data-ttu-id="a9c4d-129">Это может произойти, когда участники совместной работы используют редакторы с различными конфигурациями кодировок.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-129">This can happen when collaborators use editors with different encoding configurations.</span></span>

### <a name="how-to-tell-when-you-have-encoding-issues"></a><span data-ttu-id="a9c4d-130">Как определить наличие проблемы с кодировкой</span><span class="sxs-lookup"><span data-stu-id="a9c4d-130">How to tell when you have encoding issues</span></span>

<span data-ttu-id="a9c4d-131">Часто ошибки кодирования в скриптах представляются как ошибки синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-131">Often encoding errors present themselves as parse errors in scripts.</span></span> <span data-ttu-id="a9c4d-132">Если вы видите странные последовательности символов в скрипте, это может быть проблемой.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-132">If you find strange character sequences in your script, this can be the problem.</span></span> <span data-ttu-id="a9c4d-133">В примере ниже тире (`–`) отображается в виде символов `â€“`:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-133">In the example below, an en-dash (`–`) appears as the characters `â€“`:</span></span>

```Output
Send-MailMessage : A positional parameter cannot be found that accepts argument 'Testing FuseMail SMTP...'.
At C:\Users\<User>\<OneDrive>\Development\PowerShell\Scripts\Send-EmailUsingSmtpRelay.ps1:6 char:1
+ Send-MailMessage â€“From $from â€“To $recipient1 â€“Subject $subject  ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Send-MailMessage], ParameterBindingException
    + FullyQualifiedErrorId : PositionalParameterNotFound,Microsoft.PowerShell.Commands.SendMailMessage
```

<span data-ttu-id="a9c4d-134">Эта проблема возникает, так как VSCode кодирует символ `–` в UTF-8 при помощи байтов `0xE2 0x80 0x93`.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-134">This problem occurs because VSCode encodes the character `–` in UTF-8 as the bytes `0xE2 0x80 0x93`.</span></span>
<span data-ttu-id="a9c4d-135">Если эти байты декодируются в кодировке Windows-1252, они интерпретируются как символы `â€“`.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-135">When these bytes are decoded as Windows-1252, they are interpreted as the characters `â€“`.</span></span>

<span data-ttu-id="a9c4d-136">Некоторые странные последовательности символов, которые можно видеть:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-136">Some strange character sequences that you might see include:</span></span>

<!-- markdownlint-disable MD038 -->
- <span data-ttu-id="a9c4d-137">`â€“` вместо `–`;</span><span class="sxs-lookup"><span data-stu-id="a9c4d-137">`â€“` instead of `–`</span></span>
- <span data-ttu-id="a9c4d-138">`â€”` вместо `—`;</span><span class="sxs-lookup"><span data-stu-id="a9c4d-138">`â€”` instead of `—`</span></span>
- <span data-ttu-id="a9c4d-139">`Ã„2` вместо `Ä`;</span><span class="sxs-lookup"><span data-stu-id="a9c4d-139">`Ã„2` instead of `Ä`</span></span>
- <span data-ttu-id="a9c4d-140">`Â` вместо ` ` (неразрывный пробел);</span><span class="sxs-lookup"><span data-stu-id="a9c4d-140">`Â` instead of ` `  (a non-breaking space)</span></span>
- <span data-ttu-id="a9c4d-141">`Ã©` вместо `é`.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-141">`Ã©` instead of `é`</span></span>
<!-- markdownlint-enable MD038 -->

<span data-ttu-id="a9c4d-142">Этот удобный [справочник](https://www.i18nqa.com/debug/utf8-debug.html) перечисляет распространенные шаблоны, которые указывают на проблему между кодировками UTF-8 и Windows-1252.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-142">This handy [reference](https://www.i18nqa.com/debug/utf8-debug.html) lists the common patterns that indicate a UTF-8/Windows-1252 encoding problem.</span></span>

## <a name="how-the-powershell-extension-in-vscode-interacts-with-encodings"></a><span data-ttu-id="a9c4d-143">Взаимодействие расширения PowerShell в VSCode с кодировками</span><span class="sxs-lookup"><span data-stu-id="a9c4d-143">How the PowerShell extension in VSCode interacts with encodings</span></span>

<span data-ttu-id="a9c4d-144">Расширение PowerShell взаимодействует со скриптами несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-144">The PowerShell extension interacts with scripts in a number of ways:</span></span>

1. <span data-ttu-id="a9c4d-145">При изменении скриптов в VSCode содержимое отправляются из VSCode в расширение.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-145">When scripts are edited in VSCode, the contents are sent by VSCode to the extension.</span></span> <span data-ttu-id="a9c4d-146">[Протокол языкового сервера][] требует, чтобы это содержимое передавалось в UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-146">The [Language Server Protocol][] mandates that this content is transferred in UTF-8.</span></span> <span data-ttu-id="a9c4d-147">Таким образом, расширение не сможет получить неправильную кодировку.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-147">Therefore, it is not possible for the extension to get the wrong encoding.</span></span>
2. <span data-ttu-id="a9c4d-148">При выполнении скриптов в интегрированной консоли они считываются оболочкой PowerShell непосредственно из файла.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-148">When scripts are executed directly in the Integrated Console, they're read from the file by PowerShell directly.</span></span> <span data-ttu-id="a9c4d-149">Если кодировка PowerShell отличается от кодировки VSCode, что-нибудь здесь может пойти не так.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-149">If PowerShell's encoding differs from VSCode's, something can go wrong here.</span></span>
3. <span data-ttu-id="a9c4d-150">Когда скрипт, который открыт в VSCode, ссылается на другой скрипт, который не был открыт в VSCode, расширение загружает содержимое второго скрипта из файловой системы.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-150">When a script that is open in VSCode references another script that is not open in VSCode, the extension falls back to loading that script's content from the file system.</span></span> <span data-ttu-id="a9c4d-151">Расширение PowerShell по умолчанию использует кодировку UTF-8, но при этом применяет обнаружение [метки порядка байтов][] (BOM), чтобы выбрать правильную кодировку.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-151">The PowerShell extension defaults to UTF-8 encoding, but uses [byte-order mark][], or BOM, detection to select the correct encoding.</span></span>

<span data-ttu-id="a9c4d-152">Проблема возникает при предположении кодировки, не использующей BOM (такой как [UTF-8][] без метки порядка байтов или [Windows-1252][]).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-152">The problem occurs when assuming the encoding of BOM-less formats (like [UTF-8][] with no BOM and [Windows-1252][]).</span></span>
<span data-ttu-id="a9c4d-153">Расширение PowerShell по умолчанию использует UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-153">The PowerShell extension defaults to UTF-8.</span></span> <span data-ttu-id="a9c4d-154">Расширение не может изменить параметры кодировки в VSCode.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-154">The extension cannot change VSCode's encoding settings.</span></span>
<span data-ttu-id="a9c4d-155">Дополнительные сведения см. в разделе [Проблема № 824](https://github.com/Microsoft/vscode/issues/824).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-155">For more information, see [issue #824](https://github.com/Microsoft/vscode/issues/824).</span></span>

## <a name="choosing-the-right-encoding"></a><span data-ttu-id="a9c4d-156">Выбор подходящей кодировки</span><span class="sxs-lookup"><span data-stu-id="a9c4d-156">Choosing the right encoding</span></span>

<span data-ttu-id="a9c4d-157">Различные системы и приложения могут использовать различные кодировки:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-157">Different systems and applications can use different encodings:</span></span>

- <span data-ttu-id="a9c4d-158">В .NET Standard, в Интернете и в среде Linux теперь в основном используется кодировка UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-158">In .NET Standard, on the web, and in the Linux world, UTF-8 is now the dominant encoding.</span></span>
- <span data-ttu-id="a9c4d-159">Во многих приложениях .NET Framework используется [UTF-16][].</span><span class="sxs-lookup"><span data-stu-id="a9c4d-159">Many .NET Framework applications use [UTF-16][].</span></span> <span data-ttu-id="a9c4d-160">По историческим причинам ее иногда называют "Юникод"; сейчас этот термин относится к более широкому [стандарту](https://en.wikipedia.org/wiki/Unicode), охватывающему UTF-8 и UTF-16.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-160">For historical reasons, this is sometimes called "Unicode", a term that now refers to a broad [standard](https://en.wikipedia.org/wiki/Unicode) that includes both UTF-8 and UTF-16.</span></span>
- <span data-ttu-id="a9c4d-161">В Windows многие приложения, которые были созданы еще до распространения Юникода, по-прежнему могут по умолчанию использовать Windows-1252.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-161">On Windows, many native applications that predate Unicode continue to use Windows-1252 by default.</span></span>

<span data-ttu-id="a9c4d-162">Кодировки Юникода также используют понятие метки порядка следования байтов (BOM).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-162">Unicode encodings also have the concept of a byte-order mark (BOM).</span></span> <span data-ttu-id="a9c4d-163">BOM ставится в начале текста, чтобы декодер мог определить, какая кодировка используется в тексте.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-163">BOMs occur at the beginning of text to tell a decoder which encoding the text is using.</span></span> <span data-ttu-id="a9c4d-164">Для многобайтовых кодировок BOM также указывает [порядок следования байтов](https://en.wikipedia.org/wiki/Endianness) кодировки.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-164">For multi-byte encodings, the BOM also indicates [endianness](https://en.wikipedia.org/wiki/Endianness) of the encoding.</span></span> <span data-ttu-id="a9c4d-165">BOM представляются байтами, которые редко встречаются в тексте в Юникоде. Это позволяет сделать обоснованное предположение, что текст записан в Юникоде, если присутствует метка BOM.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-165">BOMs are designed to be bytes that rarely occur in non-Unicode text, allowing a reasonable guess that text is Unicode when a BOM is present.</span></span>

<span data-ttu-id="a9c4d-166">BOM не являются обязательными; в мире Linux они не так популярны, поскольку во всех прочих местах используется надежное соглашение UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-166">BOMs are optional and their adoption isn't as popular in the Linux world because a dependable convention of UTF-8 is used everywhere.</span></span> <span data-ttu-id="a9c4d-167">Большинство приложений Linux предполагают, что текстовый ввод кодируется в UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-167">Most Linux applications presume that text input is encoded in UTF-8.</span></span> <span data-ttu-id="a9c4d-168">Хотя многие приложения Linux могут распознавать и правильно обрабатывать BOM, некоторые этого не делают, что приводит к появлению артефактов в тексте, открываемом с помощью этих приложений.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-168">While many Linux applications will recognize and correctly handle a BOM, a number do not, leading to artifacts in text manipulated with those applications.</span></span>

<span data-ttu-id="a9c4d-169">**Таким образом**:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-169">**Therefore**:</span></span>

- <span data-ttu-id="a9c4d-170">Если вы работаете в основном с приложениями Windows и Windows PowerShell, следует предпочтительно использовать такие кодировки, как UTF-8 с BOM или UTF-16.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-170">If you work primarily with Windows applications and Windows PowerShell, you should prefer an encoding like UTF-8 with BOM or UTF-16.</span></span>
- <span data-ttu-id="a9c4d-171">Если вы работаете на разных платформах, следует отдавать предпочтение UTF-8 с BOM.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-171">If you work across platforms, you should prefer UTF-8 with BOM.</span></span>
- <span data-ttu-id="a9c4d-172">Если вы работаете главным образом в контексте Linux, следует отдавать предпочтение UTF-8 без BOM.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-172">If you work mainly in Linux-associated contexts, you should prefer UTF-8 without BOM.</span></span>
- <span data-ttu-id="a9c4d-173">Windows-1252 и latin-1 — устаревшие кодировки, которых по возможности следует избегать.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-173">Windows-1252 and latin-1 are essentially legacy encodings that you should avoid if possible.</span></span>
  <span data-ttu-id="a9c4d-174">Тем не менее некоторые приложения предыдущих версий в Windows зависят от их.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-174">However, some older Windows applications may depend on them.</span></span>
- <span data-ttu-id="a9c4d-175">Также стоит отметить, что подписывание скриптов [зависит от кодировки](https://github.com/PowerShell/PowerShell/issues/3466), то есть изменение кодировки в подписанном скрипте потребует повторного подписывания.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-175">It's also worth noting that script signing is [encoding-dependent](https://github.com/PowerShell/PowerShell/issues/3466), meaning a change of encoding on a signed script will require resigning.</span></span>

## <a name="configuring-vscode"></a><span data-ttu-id="a9c4d-176">Настройка VSCode</span><span class="sxs-lookup"><span data-stu-id="a9c4d-176">Configuring VSCode</span></span>

<span data-ttu-id="a9c4d-177">Кодировка VSCode по умолчанию — UTF-8 без метки порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-177">VSCode's default encoding is UTF-8 without BOM.</span></span>

<span data-ttu-id="a9c4d-178">Чтобы задать [Кодировка в VSCode][], перейдите к параметрам VSCode (<kbd>Ctrl</kbd>+<kbd>,</kbd>) и задайте параметр `"files.encoding"`:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-178">To set [VSCode's encoding][], go to the VSCode settings (<kbd>Ctrl</kbd>+<kbd>,</kbd>) and set the `"files.encoding"` setting:</span></span>

```json
"files.encoding": "utf8bom"
```

<span data-ttu-id="a9c4d-179">Возможны следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-179">Some possible values are:</span></span>

- <span data-ttu-id="a9c4d-180">`utf8`: [UTF-8] без метки порядка байтов</span><span class="sxs-lookup"><span data-stu-id="a9c4d-180">`utf8`: [UTF-8] without BOM</span></span>
- <span data-ttu-id="a9c4d-181">`utf8bom`: [UTF-8] с меткой порядка байтов</span><span class="sxs-lookup"><span data-stu-id="a9c4d-181">`utf8bom`: [UTF-8] with BOM</span></span>
- <span data-ttu-id="a9c4d-182">`utf16le`: [UTF-16] с прямым порядком байтов</span><span class="sxs-lookup"><span data-stu-id="a9c4d-182">`utf16le`: Little endian [UTF-16]</span></span>
- <span data-ttu-id="a9c4d-183">`utf16be`: [UTF-16] с обратным порядком байтов</span><span class="sxs-lookup"><span data-stu-id="a9c4d-183">`utf16be`: Big endian [UTF-16]</span></span>
- <span data-ttu-id="a9c4d-184">`windows1252`: [Windows-1252]</span><span class="sxs-lookup"><span data-stu-id="a9c4d-184">`windows1252`: [Windows-1252]</span></span>

<span data-ttu-id="a9c4d-185">Должен отобразиться раскрывающийся список представления графического пользовательского интерфейса или дополнение в представлении JSON.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-185">You should get a dropdown for this in the GUI view, or completions for it in the JSON view.</span></span>

<span data-ttu-id="a9c4d-186">Чтобы обеспечить автоматическое определение кодировки, если это возможно, можно также добавить следующее:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-186">You can also add the following to autodetect encoding when possible:</span></span>

```json
"files.autoGuessEncoding": true
```

<span data-ttu-id="a9c4d-187">Если вы не хотите, чтобы эти параметры влияли на все типы файлов, VSCode также позволяет задавать конфигурации для каждого языка отдельно.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-187">If you don't want these settings to affect all files types, VSCode also allows per-language configurations.</span></span> <span data-ttu-id="a9c4d-188">Создать параметр для конкретного языка можно, поместив параметры в поле `[<language-name>]`.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-188">Create a language-specific setting by putting settings in a `[<language-name>]` field.</span></span> <span data-ttu-id="a9c4d-189">Например:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-189">For example:</span></span>

```json
"[powershell]": {
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

## <a name="configuring-powershell"></a><span data-ttu-id="a9c4d-190">Настройка PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9c4d-190">Configuring PowerShell</span></span>

<span data-ttu-id="a9c4d-191">В PowerShell кодировка по умолчанию зависит от версии:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-191">PowerShell's default encoding varies depending on version:</span></span>

- <span data-ttu-id="a9c4d-192">В PowerShell 6+ кодировка по умолчанию на всех платформах — UTF-8 без метки порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-192">In PowerShell 6+, the default encoding is UTF-8 without BOM on all platforms.</span></span>
- <span data-ttu-id="a9c4d-193">В Windows PowerShell кодировка по умолчанию — обычно Windows-1252, расширение [latin-1][], которое также называется ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-193">In Windows PowerShell, the default encoding is usually Windows-1252, an extension of [latin-1][], also known as ISO 8859-1.</span></span>

<span data-ttu-id="a9c4d-194">В PowerShell 5 + можно определить кодировку по умолчанию так:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-194">In PowerShell 5+ you can find your default encoding with this:</span></span>

```powershell
[psobject].Assembly.GetTypes() | Where-Object { $_.Name -eq 'ClrFacade'} |
  ForEach-Object {
    $_.GetMethod('GetDefaultEncoding', [System.Reflection.BindingFlags]'nonpublic,static').Invoke($null, @())
  }
```

<span data-ttu-id="a9c4d-195">Следующий [скрипт](https://gist.github.com/rjmholt/3d8dd4849f718c914132ce3c5b278e0e) может использоваться для определения кодировки, которую ваш сеанс PowerShell выводит для скрипта, где нет метки порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-195">The following [script](https://gist.github.com/rjmholt/3d8dd4849f718c914132ce3c5b278e0e) can be used to determine what encoding your PowerShell session infers for a script without a BOM.</span></span>

```powershell
$badBytes = [byte[]]@(0xC3, 0x80)
$utf8Str = [System.Text.Encoding]::UTF8.GetString($badBytes)
$bytes = [System.Text.Encoding]::ASCII.GetBytes('Write-Output "') + [byte[]]@(0xC3, 0x80) + [byte[]]@(0x22)
$path = Join-Path ([System.IO.Path]::GetTempPath()) 'encodingtest.ps1'

try
{
    [System.IO.File]::WriteAllBytes($path, $bytes)

    switch (& $path)
    {
        $utf8Str
        {
            return 'UTF-8'
            break
        }

        default
        {
            return 'Windows-1252'
            break
        }
    }
}
finally
{
    Remove-Item $path
}
```

<span data-ttu-id="a9c4d-196">Можно настроить PowerShell так, чтобы использовать заданную кодировку в более общем виде с помощью параметров профиля.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-196">It's possible to configure PowerShell to use a given encoding more generally using profile settings.</span></span> <span data-ttu-id="a9c4d-197">См. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-197">See the following articles:</span></span>

- <span data-ttu-id="a9c4d-198">[Ответ [@mklement0] о кодировке PowerShell на сайте StackOverflow](https://stackoverflow.com/a/40098904).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-198">[@mklement0]'s [answer about PowerShell encoding on StackOverflow](https://stackoverflow.com/a/40098904).</span></span>
- <span data-ttu-id="a9c4d-199">[Запись блога [@rkeithhill] об обработке входных данных в UTF-8 без метки порядка байтов в PowerShell](https://rkeithhill.wordpress.com/2010/05/26/handling-native-exe-output-encoding-in-utf8-with-no-bom/).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-199">[@rkeithhill]'s [blog post about dealing with BOM-less UTF-8 input in PowerShell](https://rkeithhill.wordpress.com/2010/05/26/handling-native-exe-output-encoding-in-utf8-with-no-bom/).</span></span>

<span data-ttu-id="a9c4d-200">Заставить PowerShell использовать конкретную кодировку для входных данных невозможно.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-200">It's not possible to force PowerShell to use a specific input encoding.</span></span> <span data-ttu-id="a9c4d-201">PowerShell 5.1 и более ранние версии по умолчанию используют кодировку Windows-1252, если отсутствует BOM.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-201">PowerShell 5.1 and below default to Windows-1252 encoding when there's no BOM.</span></span> <span data-ttu-id="a9c4d-202">По причинам совместимости лучше сохранять скрипты в Юникоде с меткой порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-202">For interoperability reasons, it's best to save scripts in a Unicode format with a BOM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9c4d-203">Любые другие имеющиеся у вас инструменты для работы со скриптами PowerShell могут зависеть от выбранных параметров кодировки или преобразовывать скрипты в другую кодировку.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-203">Any other tools you have that touch PowerShell scripts may be affected by your encoding choices or re-encode your scripts to another encoding.</span></span>

### <a name="existing-scripts"></a><span data-ttu-id="a9c4d-204">Существующие скрипты</span><span class="sxs-lookup"><span data-stu-id="a9c4d-204">Existing scripts</span></span>

<span data-ttu-id="a9c4d-205">Скрипты, которые уже находятся в файловой системе, могут нуждаться в повторном кодировании в указанную вами кодировку.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-205">Scripts already on the file system may need to be re-encoded to your new chosen encoding.</span></span> <span data-ttu-id="a9c4d-206">В нижней строке VSCode вы увидите метку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-206">In the bottom bar of VSCode, you'll see the label UTF-8.</span></span> <span data-ttu-id="a9c4d-207">Щелкните ее, чтобы открыть панель действий, и выберите команду **Сохранить с кодировкой**.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-207">Click it to open the action bar and select **Save with encoding**.</span></span> <span data-ttu-id="a9c4d-208">Теперь вы можете выбрать новую кодировку для этого файла.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-208">You can now pick a new encoding for that file.</span></span> <span data-ttu-id="a9c4d-209">См. подробные инструкции в разделе [Кодировка в VSCode][].</span><span class="sxs-lookup"><span data-stu-id="a9c4d-209">See [VSCode's encoding][] for full instructions.</span></span>

<span data-ttu-id="a9c4d-210">Если вам нужно повторно кодировать несколько файлов, можно использовать следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-210">If you need to re-encode multiple files, you can use the following script:</span></span>

```powershell
Get-ChildItem *.ps1 -Recurse | ForEach-Object {
    $content = Get-Content -Path $_
    Set-Content -Path $_.Fullname -Value $content -Encoding UTF8 -PassThru -Force
}
```

### <a name="the-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="a9c4d-211">Интегрированная среда сценариев (ISE) PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9c4d-211">The PowerShell Integrated Scripting Environment (ISE)</span></span>

<span data-ttu-id="a9c4d-212">При редактировании скриптов с помощью интегрированной среды сценариев PowerShell необходимо синхронизировать здесь параметры кодировки.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-212">If you also edit scripts using the PowerShell ISE, you need to synchronize your encoding settings there.</span></span>

<span data-ttu-id="a9c4d-213">Интегрированная среда сценариев должна учитывать метку порядка байтов, но можно также использовать отражение для [задания кодировки](https://bensonxion.wordpress.com/2012/04/25/powershell-ise-default-saveas-encoding/).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-213">The ISE should honor a BOM, but it's also possible to use reflection to [set the encoding](https://bensonxion.wordpress.com/2012/04/25/powershell-ise-default-saveas-encoding/).</span></span>
<span data-ttu-id="a9c4d-214">Обратите внимание, что это значение не сохраняется между запусками.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-214">Note that this wouldn't be persisted between startups.</span></span>

### <a name="source-control-software"></a><span data-ttu-id="a9c4d-215">Система управления версиями</span><span class="sxs-lookup"><span data-stu-id="a9c4d-215">Source control software</span></span>

<span data-ttu-id="a9c4d-216">Некоторые системы управления версиями, например git, игнорируют кодировки; git отслеживает только байты.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-216">Some source control tools, such as git, ignore encodings; git just tracks the bytes.</span></span>
<span data-ttu-id="a9c4d-217">Поведение других, например Azure DevOps или Mercurial, может отличаться.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-217">Others, like Azure DevOps or Mercurial, may not.</span></span> <span data-ttu-id="a9c4d-218">Даже некоторые средства, основанные на git, полагаются на декодирование текста.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-218">Even some git-based tools rely on decoding text.</span></span>

<span data-ttu-id="a9c4d-219">Если это так, убедитесь, что вы:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-219">When this is the case, make sure you:</span></span>

- <span data-ttu-id="a9c4d-220">Настроили кодировку в системе управления версиями в соответствии с вашей конфигурацией VSCode.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-220">Configure the text encoding in your source control to match your VSCode configuration.</span></span>
- <span data-ttu-id="a9c4d-221">Сделали так, что все файлы добавляются в систему управления версиями в соответствующей кодировке.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-221">Ensure all your files are checked into source control in the relevant encoding.</span></span>
- <span data-ttu-id="a9c4d-222">Остерегайтесь изменять кодировки, полученные через систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-222">Be wary of changes to the encoding received through source control.</span></span> <span data-ttu-id="a9c4d-223">Ключевым признаком здесь будет разностный файл, который указывает, что изменения отсутствуют (так как изменены байты, но не символы).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-223">A key sign of this is a diff indicating changes but where nothing seems to have changed (because bytes have but characters have not).</span></span>

### <a name="collaborators-environments"></a><span data-ttu-id="a9c4d-224">Среды других участников</span><span class="sxs-lookup"><span data-stu-id="a9c4d-224">Collaborators' environments</span></span>

<span data-ttu-id="a9c4d-225">Настроив систему управления версиями, убедитесь также, что параметры других участников, работающих над теми файлами, к которым вы предоставляете общий доступ, не переопределяют кодировку путем повторного кодирования файлов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-225">On top of configuring source control, ensure that your collaborators on any files you share don't have settings that override your encoding by re-encoding PowerShell files.</span></span>

### <a name="other-programs"></a><span data-ttu-id="a9c4d-226">Другие программы</span><span class="sxs-lookup"><span data-stu-id="a9c4d-226">Other programs</span></span>

<span data-ttu-id="a9c4d-227">Все другие программы, которые считывают или записывают скрипты PowerShell, могут перекодировать их.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-227">Any other program that reads or writes a PowerShell script may re-encode it.</span></span>

<span data-ttu-id="a9c4d-228">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-228">Some examples are:</span></span>

- <span data-ttu-id="a9c4d-229">Использование буфера обмена для копирования и вставки скрипта.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-229">Using the clipboard to copy and paste a script.</span></span> <span data-ttu-id="a9c4d-230">Такое часто встречается в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-230">This is common in scenarios like:</span></span>
  - <span data-ttu-id="a9c4d-231">Копирование скрипта в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-231">Copying a script into a VM</span></span>
  - <span data-ttu-id="a9c4d-232">Копирование скрипта из электронной почты или с веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-232">Copying a script out of an email or webpage</span></span>
  - <span data-ttu-id="a9c4d-233">Копирование скрипта через документ Microsoft Word или PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-233">Copying a script into or out of a Microsoft Word or PowerPoint document</span></span>
- <span data-ttu-id="a9c4d-234">Другие текстовые редакторы, например:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-234">Other text editors, such as:</span></span>
  - <span data-ttu-id="a9c4d-235">Блокнот;</span><span class="sxs-lookup"><span data-stu-id="a9c4d-235">Notepad</span></span>
  - <span data-ttu-id="a9c4d-236">vim;</span><span class="sxs-lookup"><span data-stu-id="a9c4d-236">vim</span></span>
  - <span data-ttu-id="a9c4d-237">любой другой редактор скриптов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-237">Any other PowerShell script editor</span></span>
- <span data-ttu-id="a9c4d-238">Служебные программы редактирования текста, например:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-238">Text editing utilities, like:</span></span>
  - `Get-Content`/`Set-Content`/`Out-File`
  - <span data-ttu-id="a9c4d-239">Операторы перенаправления PowerShell, такие как `>` и `>>`.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-239">PowerShell redirection operators like `>` and `>>`</span></span>
  - `sed`/`awk`
- <span data-ttu-id="a9c4d-240">Программы передачи файлов, такие как:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-240">File transfer programs, like:</span></span>
  - <span data-ttu-id="a9c4d-241">Веб-браузер при скачивании скриптов.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-241">A web browser, when downloading scripts</span></span>
  - <span data-ttu-id="a9c4d-242">Общий файловый ресурс.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-242">A file share</span></span>

<span data-ttu-id="a9c4d-243">Некоторые из этих средств работают с байтами, а не с текстом, но другие позволяют настраивать кодировки.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-243">Some of these tools deal in bytes rather than text, but others offer encoding configurations.</span></span> <span data-ttu-id="a9c4d-244">В случаях, когда необходимо настроить кодировку, используйте те же параметры, что и в вашем редакторе, чтобы предотвратить возникновение проблем.</span><span class="sxs-lookup"><span data-stu-id="a9c4d-244">In those cases where you need to configure an encoding, you need to make it the same as your editor encoding to prevent problems.</span></span>

## <a name="other-resources-on-encoding-in-powershell"></a><span data-ttu-id="a9c4d-245">Другие ресурсы о кодировках в PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9c4d-245">Other resources on encoding in PowerShell</span></span>

<span data-ttu-id="a9c4d-246">Существует несколько других достойных публикаций на тему кодировок и настройки кодирования в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-246">There are a few other nice posts on encoding and configuring encoding in PowerShell that are worth a read:</span></span>

- <span data-ttu-id="a9c4d-247">[Обзор [@mklement0] о кодировке PowerShell на сайте StackOverflow](https://stackoverflow.com/questions/40098771/changing-powershells-default-output-encoding-to-utf-8).</span><span class="sxs-lookup"><span data-stu-id="a9c4d-247">[@mklement0]'s [summary of PowerShell encoding on StackOverflow](https://stackoverflow.com/questions/40098771/changing-powershells-default-output-encoding-to-utf-8)</span></span>
- <span data-ttu-id="a9c4d-248">Предыдущие проблемы с кодировками, найденные в vscode-PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a9c4d-248">Previous issues opened on vscode-PowerShell for encoding problems:</span></span>
  - [<span data-ttu-id="a9c4d-249">#1308</span><span class="sxs-lookup"><span data-stu-id="a9c4d-249">#1308</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1308)
  - [<span data-ttu-id="a9c4d-250">#1628</span><span class="sxs-lookup"><span data-stu-id="a9c4d-250">#1628</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1628)
  - [<span data-ttu-id="a9c4d-251">#1680</span><span class="sxs-lookup"><span data-stu-id="a9c4d-251">#1680</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1680)
  - [<span data-ttu-id="a9c4d-252">#1744</span><span class="sxs-lookup"><span data-stu-id="a9c4d-252">#1744</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1744)
  - [<span data-ttu-id="a9c4d-253">#1751</span><span class="sxs-lookup"><span data-stu-id="a9c4d-253">#1751</span></span>](https://github.com/PowerShell/vscode-powershell/issues/1751)
- [<span data-ttu-id="a9c4d-254">Классическая статья *Joel on Software* про Юникод</span><span class="sxs-lookup"><span data-stu-id="a9c4d-254">The classic *Joel on Software* write up about Unicode</span></span>](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)
- [<span data-ttu-id="a9c4d-255">Кодировка в .NET Standard</span><span class="sxs-lookup"><span data-stu-id="a9c4d-255">Encoding in .NET Standard</span></span>](https://github.com/dotnet/standard/issues/260#issuecomment-289549508)


[@mklement0]: https://github.com/mklement0
[@rkeithhill]: https://github.com/rkeithhill
[Windows-1252]: https://wikipedia.org/wiki/Windows-1252
[latin-1]: https://wikipedia.org/wiki/ISO/IEC_8859-1
[UTF-8]: https://wikipedia.org/wiki/UTF-8
[метки порядка байтов]: https://wikipedia.org/wiki/Byte_order_mark
[byte-order mark]: https://wikipedia.org/wiki/Byte_order_mark
[UTF-16]: https://wikipedia.org/wiki/UTF-16
[Протокол языкового сервера]: https://microsoft.github.io/language-server-protocol/
[Language Server Protocol]: https://microsoft.github.io/language-server-protocol/
[Кодировка в VSCode]: https://code.visualstudio.com/docs/editor/codebasics#_file-encoding-support
[VSCode's encoding]: https://code.visualstudio.com/docs/editor/codebasics#_file-encoding-support
