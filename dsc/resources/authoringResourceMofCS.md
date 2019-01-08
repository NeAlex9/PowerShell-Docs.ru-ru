---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Создание ресурса DSC в C#
ms.openlocfilehash: dcda36d27f2191f140eaaf209e1c85263d2cd8e1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53402411"
---
# <a name="authoring-a-dsc-resource-in-c"></a><span data-ttu-id="56f46-103">Создание ресурса DSC в C#</span><span class="sxs-lookup"><span data-stu-id="56f46-103">Authoring a DSC resource in C#</span></span>

> <span data-ttu-id="56f46-104">Область применения. Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="56f46-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="56f46-105">Как правило, настраиваемый ресурс настройки требуемого состояния (DSC) Windows PowerShell реализуется в сценарии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56f46-105">Typically, a Windows PowerShell Desired State Configuration (DSC) custom resource is implemented in a PowerShell script.</span></span> <span data-ttu-id="56f46-106">Кроме того, для реализации настраиваемого ресурса DSC можно писать командлеты на языке C#.</span><span class="sxs-lookup"><span data-stu-id="56f46-106">However, you can also implement the functionality of a DSC custom resource by writing cmdlets in C#.</span></span> <span data-ttu-id="56f46-107">Вводные сведения о написании командлетов на языке C# см. в статье [Написание командлетов Windows PowerShell](/powershell/developer/windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="56f46-107">For an introduction on writing cmdlets in C#, see [Writing a Windows PowerShell Cmdlet](/powershell/developer/windows-powershell).</span></span>

<span data-ttu-id="56f46-108">Процесс создания схемы MOF и структуры папок, импорт и применения настраиваемого ресурса DSC (кроме реализации ресурса на языке C# в форме командлетов) соответствует описанию в статье [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md).</span><span class="sxs-lookup"><span data-stu-id="56f46-108">Aside from implementing the resource in C# as cmdlets, the process of creating the MOF schema, creating the folder structure, importing and using your custom DSC resource are the same as described in [Writing a custom DSC resource with MOF](authoringResourceMOF.md).</span></span>

## <a name="writing-a-cmdlet-based-resource"></a><span data-ttu-id="56f46-109">Создание ресурса на основе командлетов</span><span class="sxs-lookup"><span data-stu-id="56f46-109">Writing a cmdlet-based resource</span></span>
<span data-ttu-id="56f46-110">В этом примере мы реализуем простой ресурс, управляющий текстовым файлом и его содержимым.</span><span class="sxs-lookup"><span data-stu-id="56f46-110">For this example, we will implement a simple resource that manages a text file and its contents.</span></span>

### <a name="writing-the-mof-schema"></a><span data-ttu-id="56f46-111">Создание схемы MOF</span><span class="sxs-lookup"><span data-stu-id="56f46-111">Writing the MOF schema</span></span>

<span data-ttu-id="56f46-112">Ниже дано определение ресурса MOF.</span><span class="sxs-lookup"><span data-stu-id="56f46-112">The following is the MOF resource definition.</span></span>

```
[ClassVersion("1.0.0"), FriendlyName("xDemoFile")]
class MSFT_XDemoFile : OMI_BaseResource
{
                [Key, Description("path")] String Path;
                [Write, Description("Should the file be present"), ValueMap{"Present","Absent"}, Values{"Present","Absent"}] String Ensure;
                [Write, Description("Contentof file.")] String Content;
};
```

### <a name="setting-up-the-visual-studio-project"></a><span data-ttu-id="56f46-113">Настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="56f46-113">Setting up the Visual Studio project</span></span>
#### <a name="setting-up-a-cmdlet-project"></a><span data-ttu-id="56f46-114">Настройка проекта командлета</span><span class="sxs-lookup"><span data-stu-id="56f46-114">Setting up a cmdlet project</span></span>

1. <span data-ttu-id="56f46-115">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="56f46-115">Open Visual Studio.</span></span>
1. <span data-ttu-id="56f46-116">Создайте проект C# и укажите имя.</span><span class="sxs-lookup"><span data-stu-id="56f46-116">Create a C# project and provide the name.</span></span>
1. <span data-ttu-id="56f46-117">Выберите в списке доступных шаблонов проектов **библиотеку классов**.</span><span class="sxs-lookup"><span data-stu-id="56f46-117">Select **Class Library** from the available project templates.</span></span>
1. <span data-ttu-id="56f46-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="56f46-118">Click **Ok**.</span></span>
1. <span data-ttu-id="56f46-119">Добавьте в проект ссылку на сборку System.Automation.Management.dll.</span><span class="sxs-lookup"><span data-stu-id="56f46-119">Add an assembly reference to System.Automation.Management.dll to your project.</span></span>
1. <span data-ttu-id="56f46-120">Измените имя сборки в соответствии с именем ресурса.</span><span class="sxs-lookup"><span data-stu-id="56f46-120">Change the assembly name to match the resource name.</span></span> <span data-ttu-id="56f46-121">В данном случае сборка должна называться **MSFT_XDemoFile**.</span><span class="sxs-lookup"><span data-stu-id="56f46-121">In this case, the assembly should be named **MSFT_XDemoFile**.</span></span>

### <a name="writing-the-cmdlet-code"></a><span data-ttu-id="56f46-122">Написание кода командлета</span><span class="sxs-lookup"><span data-stu-id="56f46-122">Writing the cmdlet code</span></span>

<span data-ttu-id="56f46-123">Следующий код на языке C# реализует командлеты **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="56f46-123">The following C# code implements the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** cmdlets.</span></span>

```C#


namespace cSharpDSCResourceExample
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Management.Automation;  // Windows PowerShell assembly.

    #region Get-TargetResource

    [OutputType(typeof(System.Collections.Hashtable))]
    [Cmdlet(VerbsCommon.Get, "TargetResource")]
    public class GetTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        /// <summary>
        /// Implement the logic to return the current state of the resource as a hashtable with keys being the resource properties
        /// and the values are the corresponding current value on the machine.
        /// </summary>
        protected override void ProcessRecord()
        {
            var currentResourceState = new Dictionary<string, string>();
            if (File.Exists(Path))
            {
                currentResourceState.Add("Ensure", "Present");

                // read current content
                string CurrentContent = "";
                using (var reader = new StreamReader(Path))
                {
                    CurrentContent = reader.ReadToEnd();
                }
                currentResourceState.Add("Content", CurrentContent);
            }
            else
            {
                currentResourceState.Add("Ensure", "Absent");
                currentResourceState.Add("Content", "");
            }
            // write the hashtable in the PS console.
            WriteObject(currentResourceState);
        }
    }

    # endregion

    #region Set-TargetResource
    [OutputType(typeof(void))]
    [Cmdlet(VerbsCommon.Set, "TargetResource")]
    public class SetTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        [Parameter(Mandatory = false)]

        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure {
            get
            {
                // set the default to present.
               return (this._ensure ?? "Present") ;
            }
            set
            {
                this._ensure = value;
            }
        }

        [Parameter(Mandatory = false)]
        public string Content {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }

        private string _ensure;
        private string _content;

        /// <summary>
        /// Implement the logic to set the state of the machine to the desired state.
        /// </summary>
        protected override void ProcessRecord()
        {
            WriteVerbose(string.Format("Running set with parameters {0}{1}{2}", Path, Ensure, Content));
            if (File.Exists(Path))
            {
                if (Ensure.Equals("absent", StringComparison.InvariantCultureIgnoreCase))
                {
                    File.Delete(Path);
                }
                else
                {
                    // file already exist and ensure "present" is specified. start writing the content to a file
                    if (!string.IsNullOrEmpty(Content))
                    {
                        string existingContent = null;
                        using (var reader = new StreamReader(Path))
                        {
                            existingContent = reader.ReadToEnd();
                        }
                        // check if the content of the file mathes the content passed
                        if (!existingContent.Equals(Content, StringComparison.InvariantCultureIgnoreCase))
                        {
                            WriteVerbose("Existing content did not match with desired content updating the content of the file");
                            using (var writer = new StreamWriter(Path))
                            {
                                writer.Write(Content);
                                writer.Flush();
                            }
                        }
                    }
                }

            }
            else
            {
                if (Ensure.Equals("present", StringComparison.InvariantCultureIgnoreCase))
                {
                    // if nothing is passed for content just write "" otherwise write the content passed.
                    using (var writer = new StreamWriter(Path))
                    {
                        WriteVerbose(string.Format("Creating a file under path {0} with content {1}", Path, Content));
                        writer.Write(Content);
                    }
                }

            }

            /* if you need to reboot the VM. please add the following two line of code.
            PSVariable DscMachineStatus = new PSVariable("DSCMachineStatus", 1, ScopedItemOptions.AllScope);
            this.SessionState.PSVariable.Set(DscMachineStatus);
             */

        }

    }

    # endregion

    #region Test-TargetResource

    [Cmdlet("Test", "TargetResource")]
    [OutputType(typeof(Boolean))]
    public class TestTargetResource : PSCmdlet
    {
        [Parameter(Mandatory = true)]
        public string Path { get; set; }

        [Parameter(Mandatory = false)]

        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure
        {
            get
            {
                // set the default to present.
                return (this._ensure ?? "Present");
            }
            set
            {
                this._ensure = value;
            }
        }

        [Parameter(Mandatory = false)]
        public string Content
        {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }

        private string _ensure;
        private string _content;

        /// <summary>
        /// Return a boolean value which indicates wheather the current machine is in desired state or not.
        /// </summary>
        protected override void ProcessRecord()
        {
            if (File.Exists(Path))
            {
                if( Ensure.Equals("absent", StringComparison.InvariantCultureIgnoreCase))
                {
                    WriteObject(false);
                }
                else
                {
                    // check if the content matches

                    string existingContent = null;
                    using (var stream = new StreamReader(Path))
                    {
                        existingContent = stream.ReadToEnd();
                    }

                    WriteObject(Content.Equals(existingContent, StringComparison.InvariantCultureIgnoreCase));
                }
            }
            else
            {
                WriteObject(Ensure.Equals("Absent", StringComparison.InvariantCultureIgnoreCase));
            }
        }
    }

    # endregion

}
```

### <a name="deploying-the-resource"></a><span data-ttu-id="56f46-124">Развертывание ресурса</span><span class="sxs-lookup"><span data-stu-id="56f46-124">Deploying the resource</span></span>

<span data-ttu-id="56f46-125">Скомпилированный DLL-файл необходимо сохранить в структуре файлов аналогично ресурсу на основе сценария.</span><span class="sxs-lookup"><span data-stu-id="56f46-125">The compiled dll file should be saved in a file structure similar to a script-based resource.</span></span> <span data-ttu-id="56f46-126">Ниже показана структура папок для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="56f46-126">The following is the folder structure for this resource.</span></span>

```
$env: psmodulepath (folder)
    |- MyDscResources (folder)
        |- MyDscResources.psd1 (file, required)
        |- DSCResources (folder)
            |- MSFT_XDemoFile (folder)
                |- MSFT_XDemoFile.psd1 (file, optional)
                |- MSFT_XDemoFile.dll (file, required)
                |- MSFT_XDemoFile.schema.mof (file, required)
```

### <a name="see-also"></a><span data-ttu-id="56f46-127">См. также</span><span class="sxs-lookup"><span data-stu-id="56f46-127">See Also</span></span>
#### <a name="concepts"></a><span data-ttu-id="56f46-128">Концепции</span><span class="sxs-lookup"><span data-stu-id="56f46-128">Concepts</span></span>
[<span data-ttu-id="56f46-129">Написание пользовательских ресурсов DSC с использованием MOF</span><span class="sxs-lookup"><span data-stu-id="56f46-129">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
#### <a name="other-resources"></a><span data-ttu-id="56f46-130">Прочие ресурсы</span><span class="sxs-lookup"><span data-stu-id="56f46-130">Other Resources</span></span>
[<span data-ttu-id="56f46-131">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="56f46-131">Writing a Windows PowerShell Cmdlet</span></span>](/powershell/developer/windows-powershell)