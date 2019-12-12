---
title: Как переопределить методы обработки ввода | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1a1ad921-5816-4937-acf1-ed4760fae740
caps.latest.revision: 8
ms.openlocfilehash: cfee55576518cf9ce38501192872ce94054f5213
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72364473"
---
# <a name="how-to-override-input-processing-methods"></a><span data-ttu-id="76643-102">Как переопределить методы обработки входных данных</span><span class="sxs-lookup"><span data-stu-id="76643-102">How to Override Input Processing Methods</span></span>

<span data-ttu-id="76643-103">В этих примерах показано, как перезаписать методы обработки ввода в командлете.</span><span class="sxs-lookup"><span data-stu-id="76643-103">These examples show how to overwrite the input processing methods within a cmdlet.</span></span> <span data-ttu-id="76643-104">Эти методы используются для выполнения следующих операций:</span><span class="sxs-lookup"><span data-stu-id="76643-104">These methods are used to perform the following operations:</span></span>

- <span data-ttu-id="76643-105">Метод [System. Management. Automation. командлет. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) используется для выполнения одноразовых операций запуска, допустимых для всех объектов, обрабатываемых командлетом.</span><span class="sxs-lookup"><span data-stu-id="76643-105">The [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method is used to perform one-time startup operations that are valid for all the objects processed by the cmdlet.</span></span> <span data-ttu-id="76643-106">Среда выполнения Windows PowerShell вызывает этот метод только один раз.</span><span class="sxs-lookup"><span data-stu-id="76643-106">The Windows PowerShell runtime calls this method only once.</span></span>

- <span data-ttu-id="76643-107">Метод [System. Management. Automation. командлет. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) используется для обработки объектов, передаваемых в командлет.</span><span class="sxs-lookup"><span data-stu-id="76643-107">The [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method is used to process the objects passed to the cmdlet.</span></span> <span data-ttu-id="76643-108">Среда выполнения Windows PowerShell вызывает этот метод для каждого объекта, передаваемого в командлет.</span><span class="sxs-lookup"><span data-stu-id="76643-108">The Windows PowerShell runtime calls this method for each object passed to the cmdlet.</span></span>

- <span data-ttu-id="76643-109">Метод [System. Management. Automation. командлет. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) используется для выполнения операций однократной завершающей обработки.</span><span class="sxs-lookup"><span data-stu-id="76643-109">The [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method is used to perform one-time post processing operations.</span></span> <span data-ttu-id="76643-110">Среда выполнения Windows PowerShell вызывает этот метод только один раз.</span><span class="sxs-lookup"><span data-stu-id="76643-110">The Windows PowerShell runtime calls this method only once.</span></span>

## <a name="to-override-the-beginprocessing-method"></a><span data-ttu-id="76643-111">Переопределение метода BeginProcessing</span><span class="sxs-lookup"><span data-stu-id="76643-111">To override the BeginProcessing method</span></span>

- <span data-ttu-id="76643-112">Объявите защищенное переопределение метода [System. Management. Automation. командлета. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) .</span><span class="sxs-lookup"><span data-stu-id="76643-112">Declare a protected override of the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method.</span></span>

<span data-ttu-id="76643-113">Следующий класс выводит образец сообщения.</span><span class="sxs-lookup"><span data-stu-id="76643-113">The following class prints a sample message.</span></span> <span data-ttu-id="76643-114">Чтобы использовать этот класс, измените глагол и существительное в атрибуте командлета, измените имя класса, чтобы отразить новую глагол и существительное, а затем добавьте функциональные возможности, необходимые для переопределения метода [System. Management. Automation. командлет. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) .</span><span class="sxs-lookup"><span data-stu-id="76643-114">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "BeginProcessingClass")]
public class TestBeginProcessingClassTemplate : Cmdlet
{
  // Override the BeginProcessing method to add preprocessing
  //operations to the cmdlet.
  protected override void BeginProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the BeginProcessing template.");
  }
}
```

## <a name="to-override-the-processrecord-method"></a><span data-ttu-id="76643-115">Переопределение метода ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="76643-115">To override the ProcessRecord method</span></span>

- <span data-ttu-id="76643-116">Объявите защищенное переопределение метода [System. Management. Automation. командлета. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) .</span><span class="sxs-lookup"><span data-stu-id="76643-116">Declare a protected override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

<span data-ttu-id="76643-117">Следующий класс выводит образец сообщения.</span><span class="sxs-lookup"><span data-stu-id="76643-117">The following class prints a sample message.</span></span> <span data-ttu-id="76643-118">Чтобы использовать этот класс, измените глагол и существительное в атрибуте командлета, измените имя класса, чтобы отразить новую глагол и существительное, а затем добавьте функциональные возможности, необходимые для переопределения метода [System. Management. Automation. командлет. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) .</span><span class="sxs-lookup"><span data-stu-id="76643-118">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "ProcessRecordClass")]
public class TestProcessRecordClassTemplate : Cmdlet
{
    // Override the ProcessRecord method to add processing
    //operations to the cmdlet.
    protected override void ProcessRecord()
    {
        // Replace the WriteObject method with the logic required
        // by your cmdlet. It is used here to generate the following
        // output:
        // "This is a test of the ProcessRecord template."
        WriteObject("This is a test of the ProcessRecord template.");
    }
}

```

## <a name="to-override-the-endprocessing-method"></a><span data-ttu-id="76643-119">Переопределение метода EndProcessing</span><span class="sxs-lookup"><span data-stu-id="76643-119">To override the EndProcessing method</span></span>

- <span data-ttu-id="76643-120">Объявите защищенное переопределение метода [System. Management. Automation. командлет. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) .</span><span class="sxs-lookup"><span data-stu-id="76643-120">Declare a protected override of the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span>

<span data-ttu-id="76643-121">Следующий класс выводит пример.</span><span class="sxs-lookup"><span data-stu-id="76643-121">The following class prints a sample.</span></span> <span data-ttu-id="76643-122">Чтобы использовать этот класс, измените глагол и существительное в атрибуте командлета, измените имя класса, чтобы отразить новую глагол и существительное, а затем добавьте функциональные возможности, необходимые для переопределения метода [System. Management. Automation. командлет. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) .</span><span class="sxs-lookup"><span data-stu-id="76643-122">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "EndProcessingClass")]
public class TestEndProcessingClassTemplate : Cmdlet
{
  // Override the EndProcessing method to add postprocessing
  //operations to the cmdlet.
  protected override void EndProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the EndProcessing template.");
  }
}
```

## <a name="see-also"></a><span data-ttu-id="76643-123">См. также:</span><span class="sxs-lookup"><span data-stu-id="76643-123">See Also</span></span>

[<span data-ttu-id="76643-124">System. Management. Automation. командлет. BeginProcessing</span><span class="sxs-lookup"><span data-stu-id="76643-124">System.Management.Automation.Cmdlet.BeginProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[<span data-ttu-id="76643-125">System. Management. Automation. командлет. EndProcessing</span><span class="sxs-lookup"><span data-stu-id="76643-125">System.Management.Automation.Cmdlet.EndProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[<span data-ttu-id="76643-126">System. Management. Automation. командлет. ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="76643-126">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[<span data-ttu-id="76643-127">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="76643-127">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
