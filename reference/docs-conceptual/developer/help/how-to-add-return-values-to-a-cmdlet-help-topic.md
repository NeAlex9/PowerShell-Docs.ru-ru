---
title: Добавление возвращаемых значений в раздел справки по командлетам | Документация Майкрософт
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a52ab737-753c-4d04-8af7-758d5c805e18
caps.latest.revision: 7
ms.openlocfilehash: a5618b72827d8ef70201437c4a99ea8bf68cdfd3
ms.sourcegitcommit: 173556307d45d88de31086ce776770547eece64c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83565549"
---
# <a name="how-to-add-return-values-to-a-cmdlet-help-topic"></a><span data-ttu-id="a8f8b-102">Как добавить возвращаемые значения в раздел справки для командлета</span><span class="sxs-lookup"><span data-stu-id="a8f8b-102">How to Add Return Values to a Cmdlet Help Topic</span></span>

<span data-ttu-id="a8f8b-103">В этом разделе описывается добавление раздела OUTPUTs в раздел справки Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-103">This section describes how to add an OUTPUTS section to a Windows PowerShell® cmdlet Help topic.</span></span> <span data-ttu-id="a8f8b-104">В разделе OUTPUTs перечислены классы .NET объектов, которые командлет возвращает или передает по конвейеру.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-104">The OUTPUTS section lists the .NET classes of objects that the cmdlet returns or passes down the pipeline.</span></span>

<span data-ttu-id="a8f8b-105">Количество классов, которые можно добавить в раздел OUTPUTs, не ограничено.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-105">There is no limit to the number of classes that you can add to the OUTPUTS section.</span></span> <span data-ttu-id="a8f8b-106">Типы возвращаемых данных командлета заключаются в \< команду: ретурнвалуес> node с каждым классом, заключенным в \< команду: ReturnValue> элемент.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-106">The return types of a cmdlet are enclosed in a \<command:returnValues> node, with each class enclosed in a \<command:returnValue> element.</span></span>

<span data-ttu-id="a8f8b-107">Если командлет не создает никаких выходных данных, используйте этот раздел, чтобы указать, что выходные данные отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-107">If a cmdlet does not generate any output, use this section to indicate that there is no output.</span></span> <span data-ttu-id="a8f8b-108">Например, вместо имени класса напишите «None» и укажите краткое объяснение.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-108">For example, in place of the class name, write "None" and provide a brief explanation.</span></span> <span data-ttu-id="a8f8b-109">Если командлет создает выходные условия, используйте этот узел для объяснения условий и описания условного вывода.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-109">If the cmdlet generates output conditionally, use this node to explain the conditions and describe the conditional output.</span></span>

<span data-ttu-id="a8f8b-110">Схема включает в себя два \< элемента MAML: description> в каждой \< команде: ReturnValue> элемент.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-110">The schema includes two \<maml:description> elements in each \<command:returnValue> element.</span></span> <span data-ttu-id="a8f8b-111">Однако `Get-Help` командлет отображает только содержимое \< команды: ReturnValue>/ \< maml: Description> элемент.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-111">However, the `Get-Help` cmdlet displays only the content of the \<command:returnValue>/\<maml:description> element.</span></span>

<span data-ttu-id="a8f8b-112">Начиная с Windows PowerShell 3,0, `Get-Help` командлет отображает содержимое \< элемента MAML: URI>.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-112">Beginning in Windows PowerShell 3.0, the `Get-Help` cmdlet displays the content of the \<maml:uri> element.</span></span> <span data-ttu-id="a8f8b-113">Этот элемент позволяет направить пользователей в разделы, описывающие класс .NET.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-113">This element lets you direct users to topics that describe the .NET class.</span></span>

<span data-ttu-id="a8f8b-114">В следующем коде XML показан \< узел MAML: ретурнвалуес>.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-114">The following XML shows the \<maml:returnValues> node.</span></span>

```xml
<command:returnValues>
  <command:returnValue>
    <dev:type>
      <maml:name> Class Name </maml:name>
      <maml:uri>  URI of a topic that describes the class </maml:uri>
      <maml:description/>
    </dev:type>
    <maml:description>
       <maml:para> Brief description <maml:para>

</maml:description>
  </command: returnValue>
</command: returnValues>
```

<span data-ttu-id="a8f8b-115">В следующем коде XML показан пример использования \< узла MAML: ретурнвалуес> для документирования типа выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a8f8b-115">The following XML shows an example of using the \<maml:returnValues> node to document an output type.</span></span>

```xml
<command:returnValues>
  <command:returnValue>
    <dev:type>
      <maml:name> System.DateTime </maml:name>
      <maml:uri>  https://msdn.microsoft.com/library/system.datetime.aspx </maml:uri>
      <maml:description/>
    </dev:type>
    <maml:description>
      <maml:para> Get-Date returns a DateTime object. <maml:para>
    </maml:description>
  </command: returnValue>
</command: returnValues>
```
