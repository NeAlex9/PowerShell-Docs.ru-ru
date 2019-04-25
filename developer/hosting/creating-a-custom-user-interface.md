---
title: Создание собственного пользовательского интерфейса | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d7286443-eed4-43d5-b809-50cdcdcba088
caps.latest.revision: 4
ms.openlocfilehash: 23518c625fe1138e1bd2bcc895274cb21d7daf8a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083048"
---
# <a name="creating-a-custom-user-interface"></a><span data-ttu-id="41a62-102">Создание собственного пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="41a62-102">Creating a custom user interface</span></span>

<span data-ttu-id="41a62-103">Windows PowerShell предоставляет абстрактные классы и интерфейсы, которые позволяют создавать пользовательские интерактивного пользовательского интерфейса, на котором размещена подсистема Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41a62-103">Windows PowerShell provides abstract classes and interfaces that allow you to create a custom interactive UI that hosts the Windows PowerShell engine.</span></span> <span data-ttu-id="41a62-104">Чтобы создать настраиваемый пользовательский Интерфейс, необходимо реализовать [System.Management.Automation.Host.PSHost](/dotnet/api/System.Management.Automation.Host.PSHost) класса.</span><span class="sxs-lookup"><span data-stu-id="41a62-104">To create a custom UI, you must implement the [System.Management.Automation.Host.PSHost](/dotnet/api/System.Management.Automation.Host.PSHost) class.</span></span> <span data-ttu-id="41a62-105">При желании вы также можете реализовать [System.Management.Automation.Host.Pshostrawuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostRawUserInterface)и [System.Management.Automation.Host.Pshostuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface) классов и [System.Management.Automation.Host.Ihostsupportsinteractivesession](/dotnet/api/System.Management.Automation.Host.IHostSupportsInteractiveSession) и [System.Management.Automation.Host.Ihostuisupportsmultiplechoiceselection](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection) интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="41a62-105">Optionally, you can also implement the [System.Management.Automation.Host.Pshostrawuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostRawUserInterface)and [System.Management.Automation.Host.Pshostuserinterface](/dotnet/api/System.Management.Automation.Host.PSHostUserInterface) classes, and the [System.Management.Automation.Host.Ihostsupportsinteractivesession](/dotnet/api/System.Management.Automation.Host.IHostSupportsInteractiveSession) and [System.Management.Automation.Host.Ihostuisupportsmultiplechoiceselection](/dotnet/api/System.Management.Automation.Host.IHostUISupportsMultipleChoiceSelection) interfaces.</span></span>
