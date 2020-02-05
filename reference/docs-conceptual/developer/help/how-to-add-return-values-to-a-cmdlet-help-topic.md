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
ms.openlocfilehash: ad0fe5c63b145c681f14328d5ef5a8784a035e26
ms.sourcegitcommit: bc9a4904c2b1561386d748fc9ac242699d2f1694
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/04/2020
ms.locfileid: "76995934"
---
# <a name="how-to-add-return-values-to-a-cmdlet-help-topic"></a><span data-ttu-id="c4fb7-102">Как добавить возвращаемые значения в раздел справки для командлета</span><span class="sxs-lookup"><span data-stu-id="c4fb7-102">How to Add Return Values to a Cmdlet Help Topic</span></span>

<span data-ttu-id="c4fb7-103">В этом разделе описывается добавление раздела OUTPUTs в раздел справки Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-103">This section describes how to add an OUTPUTS section to a Windows PowerShell® cmdlet Help topic.</span></span> <span data-ttu-id="c4fb7-104">В разделе OUTPUTs перечислены классы .NET объектов, которые командлет возвращает или передает по конвейеру.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-104">The OUTPUTS section lists the .NET classes of objects that the cmdlet returns or passes down the pipeline.</span></span>

<span data-ttu-id="c4fb7-105">Количество классов, которые можно добавить в раздел OUTPUTs, не ограничено.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-105">There is no limit to the number of classes that you can add to the OUTPUTS section.</span></span> <span data-ttu-id="c4fb7-106">Типы возвращаемых данных командлета заключаются в \<команду: Ретурнвалуес > node с каждым классом, заключенным в \<ную команду: returnValue > элемент.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-106">The return types of a cmdlet are enclosed in a \<command:returnValues> node, with each class enclosed in a \<command:returnValue> element.</span></span>

<span data-ttu-id="c4fb7-107">Если командлет не создает никаких выходных данных, используйте этот раздел, чтобы указать, что выходные данные отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-107">If a cmdlet does not generate any output, use this section to indicate that there is no output.</span></span> <span data-ttu-id="c4fb7-108">Например, вместо имени класса напишите «None» и укажите краткое объяснение.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-108">For example, in place of the class name, write "None" and provide a brief explanation.</span></span> <span data-ttu-id="c4fb7-109">Если командлет создает выходные условия, используйте этот узел для объяснения условий и описания условного вывода.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-109">If the cmdlet generates output conditionally, use this node to explain the conditions and describe the conditional output.</span></span>

<span data-ttu-id="c4fb7-110">Схема включает в себя два \<MAML: Description > элементов в каждой команде \<: returnValue > элемент.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-110">The schema includes two \<maml:description> elements in each \<command:returnValue> element.</span></span> <span data-ttu-id="c4fb7-111">Однако командлет `Get-Help` отображает только содержимое команды \<: returnValue >/\<MAML: Description > элемент.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-111">However, the `Get-Help` cmdlet displays only the content of the \<command:returnValue>/\<maml:description> element.</span></span>

<span data-ttu-id="c4fb7-112">Начиная с Windows PowerShell 3,0, командлет `Get-Help` отображает содержимое элемента > \<MAML: URI.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-112">Beginning in Windows PowerShell 3.0, the `Get-Help` cmdlet displays the content of the \<maml:uri> element.</span></span> <span data-ttu-id="c4fb7-113">Этот элемент позволяет направить пользователей в разделы, описывающие класс .NET.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-113">This element lets you direct users to topics that describe the .NET class.</span></span>

<span data-ttu-id="c4fb7-114">В следующем коде XML показан узел \<MAML: Ретурнвалуес >.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-114">The following XML shows the \<maml:returnValues> node.</span></span>

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

<span data-ttu-id="c4fb7-115">В следующем коде XML показан пример использования узла \<MAML: Ретурнвалуес > для документирования типа выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c4fb7-115">The following XML shows an example of using the \<maml:returnValues> node to document an output type.</span></span>

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



