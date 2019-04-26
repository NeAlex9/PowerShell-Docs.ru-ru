---
title: Том, какое имя CAB-файл обновляемой справки | Документация Майкрософт
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: de302da0-c17a-4d31-a8ef-14a626738993
caps.latest.revision: 7
ms.openlocfilehash: 0b58d5ee19a85bed26bc6549ced48b890cd62f64
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082368"
---
# <a name="how-to-name-an-updatable-help-cab-file"></a><span data-ttu-id="31047-102">Как назвать CAB-файл обновляемой справки</span><span class="sxs-lookup"><span data-stu-id="31047-102">How to Name an Updatable Help CAB File</span></span>

<span data-ttu-id="31047-103">В этом разделе описывается формат обязательное имя CAB-файл обновляемой справки (. Файлы CAB-файла).</span><span class="sxs-lookup"><span data-stu-id="31047-103">This topic explains the required name format for the Updatable Help cabinet (.CAB) files.</span></span>

## <a name="how-to-name-an-updatable-help-cab-file"></a><span data-ttu-id="31047-104">Как назвать CAB-файл обновляемой справки</span><span class="sxs-lookup"><span data-stu-id="31047-104">How to Name an Updatable Help CAB File</span></span>

<span data-ttu-id="31047-105">Обновляемые CAB-файл (. Файл CAB) должен иметь имя в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="31047-105">A Updatable cabinet (.CAB) file must have a name with the following format.</span></span>

`<ModuleName>_<ModuleGUID>_<UICulture>_HelpContent.cab`

<span data-ttu-id="31047-106">Далее приведены элементы с именем.</span><span class="sxs-lookup"><span data-stu-id="31047-106">The elements of the name are as follows.</span></span>

<span data-ttu-id="31047-107">ModuleName значение из **имя** свойство **ModuleInfo** объекта, [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) командлетом.</span><span class="sxs-lookup"><span data-stu-id="31047-107">ModuleName The value of the **Name** property of the **ModuleInfo** object that the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet returns.</span></span>

<span data-ttu-id="31047-108">ModuleGUID значение из **GUID** ключа в манифесте модуля.</span><span class="sxs-lookup"><span data-stu-id="31047-108">ModuleGUID The value of the **GUID** key in the module manifest.</span></span>

<span data-ttu-id="31047-109">Культура пользовательского интерфейса UICulture файлы справки в CAB-файл.</span><span class="sxs-lookup"><span data-stu-id="31047-109">UICulture The UI culture of the help files in the CAB file.</span></span> <span data-ttu-id="31047-110">Это значение должно соответствовать значение одного из **UICulture** элементов в XML-файл HelpInfo для модуля.</span><span class="sxs-lookup"><span data-stu-id="31047-110">This value must match the value of one of the **UICulture** elements in the HelpInfo XML file for the module.</span></span>

<span data-ttu-id="31047-111">Например если имя модуля «TestModule», идентификатор GUID модуля 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9 и язык и региональные параметры пользовательского интерфейса — «en US», имя CAB-файл будет иметь:</span><span class="sxs-lookup"><span data-stu-id="31047-111">For example, if the module name is "TestModule," the module GUID is 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, and the UI culture is "en-US", the name of the CAB file would be:</span></span>

`TestModule_9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9_en-US_HelpContent.cab`