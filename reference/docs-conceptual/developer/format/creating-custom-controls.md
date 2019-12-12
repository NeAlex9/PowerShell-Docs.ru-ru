---
title: Создание настраиваемых элементов управления | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3baa406-cd33-4420-be5a-07ef09d93480
caps.latest.revision: 8
ms.openlocfilehash: 3504ab1d974c55e9279172d0e851961474ccb926
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72363383"
---
# <a name="creating-custom-controls"></a><span data-ttu-id="abd9f-102">Создание пользовательских элементов управления</span><span class="sxs-lookup"><span data-stu-id="abd9f-102">Creating Custom Controls</span></span>

<span data-ttu-id="abd9f-103">Пользовательские элементы управления — это наиболее гибкие компоненты файла форматирования.</span><span class="sxs-lookup"><span data-stu-id="abd9f-103">Custom controls are the most flexible components of a formatting file.</span></span> <span data-ttu-id="abd9f-104">В отличие от таблиц, списков и широких представлений, определяющих формальную структуру данных, например таблицу данных, пользовательские элементы управления позволяют определить способ отображения отдельного фрагмента данных.</span><span class="sxs-lookup"><span data-stu-id="abd9f-104">Unlike table, list, and wide views that define a formal structure of data, such as a table of data, custom controls allow you to define how an individual piece of data is displayed.</span></span> <span data-ttu-id="abd9f-105">Можно определить общий набор пользовательских элементов управления, доступных для всех представлений файла форматирования, можно определить пользовательские элементы управления, доступные для конкретного представления, или определить набор элементов управления, доступных группе объектов.</span><span class="sxs-lookup"><span data-stu-id="abd9f-105">You can define a common set of custom controls that are available to all the views of the formatting file, you can define custom controls that are available to a specific view, or you can define a set of controls that are available to a group of objects.</span></span>

## <a name="custom-control-example"></a><span data-ttu-id="abd9f-106">Пример пользовательского элемента управления</span><span class="sxs-lookup"><span data-stu-id="abd9f-106">Custom Control Example</span></span>

<span data-ttu-id="abd9f-107">В следующем примере показан пользовательский элемент управления, определенный в файле Certificates. Format. ps1xml.</span><span class="sxs-lookup"><span data-stu-id="abd9f-107">The following example shows a custom control that is defined in the Certificates.Format.ps1xml file.</span></span> <span data-ttu-id="abd9f-108">Этот пользовательский элемент управления используется для разделения объектов [System. Management. Automation. Signature](/dotnet/api/System.Management.Automation.Signature) , отображаемых в табличном представлении.</span><span class="sxs-lookup"><span data-stu-id="abd9f-108">This custom control is used to separate the [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) objects displayed in a table view.</span></span>

```xml
<Controls>
  <Control>
    <Name>SignatureTypes-GroupingFormat</Name>
    <CustomControl>
      <CustomEntries>
        <CustomEntry>
          <CustomItem>
            <Frame>
              <LeftIndent>4</LeftIndent>
              <CustomItem>
                <Text AssemblyName="System.Management.Automation" BaseName="FileSystemProviderStrings"
                  ResourceId="DirectoryDisplayGrouping"/>
                <ExpressionBinding>
                  <ScriptBlock>split-path $_.Path</ScriptBlock>
                </ExpressionBinding>
                <NewLine/>
              </CustomItem>
            </Frame>
          </CustomItem>
        </CustomEntry>
      </CustomEntries>
    </CustomControl>
  </Control>
</Controls>

```

## <a name="see-also"></a><span data-ttu-id="abd9f-109">См. также:</span><span class="sxs-lookup"><span data-stu-id="abd9f-109">See Also</span></span>

[<span data-ttu-id="abd9f-110">Написание файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="abd9f-110">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
