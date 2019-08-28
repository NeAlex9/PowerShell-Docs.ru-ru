---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Использование сервера отчетов DSC
ms.openlocfilehash: 1ccd4f96b782b41b7d7c953735cb41b3ba3d2bce
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986545"
---
# <a name="using-a-dsc-report-server"></a><span data-ttu-id="906ba-103">Использование сервера отчетов DSC</span><span class="sxs-lookup"><span data-stu-id="906ba-103">Using a DSC report server</span></span>

<span data-ttu-id="906ba-104">Область применения. Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="906ba-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="906ba-105">Опрашивающий сервер (компонент Windows *служба DSC*) — поддерживаемый компонент Windows Server, но реализация новых функций и возможностей для него не планируется.</span><span class="sxs-lookup"><span data-stu-id="906ba-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="906ba-106">Рекомендуется начать перенос управляемых клиентов на [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (включает возможности опрашивающего сервера в Windows Server) или на одно из решений сообщества, указанных [в следующем списке](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="906ba-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>
>
> [!NOTE]
> <span data-ttu-id="906ba-107">Сервер отчетов, описанный в этой статье, недоступен в PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="906ba-107">The report server described in this topic is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="906ba-108">В локальном диспетчере конфигураций (LCM) узла можно настроить отправку отчетов о состоянии конфигурации на опрашивающий сервер, которые затем можно запросить для извлечения содержащихся в них данных.</span><span class="sxs-lookup"><span data-stu-id="906ba-108">The Local Configuration Manager (LCM) of a node can be configured to send reports about its configuration status to a pull server, which can then be queried to retrieve that data.</span></span> <span data-ttu-id="906ba-109">Каждый раз при проверке и применении конфигурации узел отправляет отчет на сервер отчетов.</span><span class="sxs-lookup"><span data-stu-id="906ba-109">Each time the node checks and applies a configuration, it sends a report to the report server.</span></span> <span data-ttu-id="906ba-110">Эти отчеты хранятся в базе данных на сервере, и их можно извлечь, вызвав веб-службу отчетов.</span><span class="sxs-lookup"><span data-stu-id="906ba-110">These reports are stored in a database on the server, and can be retrieved by calling the reporting web service.</span></span> <span data-ttu-id="906ba-111">Каждый отчет содержит сведения, например перечень примененных конфигураций и данные о том, успешно ли они были выполнены, использованные ресурсы, любые произошедшие ошибки, а также время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="906ba-111">Each report contains information such as what configurations were applied and whether they succeeded, the resources used, any errors that were thrown, and start and finish times.</span></span>

## <a name="configuring-a-node-to-send-reports"></a><span data-ttu-id="906ba-112">Настройка узла для отправки отчетов</span><span class="sxs-lookup"><span data-stu-id="906ba-112">Configuring a node to send reports</span></span>

<span data-ttu-id="906ba-113">Запросить на узле отправку отчетов на сервер можно с помощью блока **ReportServerWeb** в конфигурации LCM узла (сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](../managing-nodes/metaConfig.md)).</span><span class="sxs-lookup"><span data-stu-id="906ba-113">You tell a node to send reports to a server by using a **ReportServerWeb** block in the node's LCM configuration (for information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md)).</span></span> <span data-ttu-id="906ba-114">Сервер, на который узел отправляет отчеты, необходимо настроить как опрашивающий веб-сервер (отправлять отчеты в общий ресурс SMB невозможно).</span><span class="sxs-lookup"><span data-stu-id="906ba-114">The server to which the node sends reports must be set up as a web pull server (you cannot send reports to an SMB share).</span></span> <span data-ttu-id="906ba-115">Сведения о настройке опрашивающего сервера см. в разделе [Настройка опрашивающего веб-сервера DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="906ba-115">For information about setting up a pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span> <span data-ttu-id="906ba-116">Сервер отчетов может быть той же службой, в которой узел извлекает конфигурации и получает ресурсы, или другой службой.</span><span class="sxs-lookup"><span data-stu-id="906ba-116">The report server can be the same service from which the node pulls configurations and gets resources, or it can be a different service.</span></span>

<span data-ttu-id="906ba-117">В блоке **ReportServerWeb** укажите URL-адрес опрашивающей службы и ключ регистрации, известный серверу.</span><span class="sxs-lookup"><span data-stu-id="906ba-117">In the **ReportServerWeb** block, you specify the URL of the pull service and a registration key that is known to the server.</span></span>

<span data-ttu-id="906ba-118">Следующая конфигурация настраивает на узле извлечение конфигураций из службы и отправку отчетов в службу на другом сервере.</span><span class="sxs-lookup"><span data-stu-id="906ba-118">The following configuration configures a node to pull configurations from one service, and send reports to a service on a different server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration ReportClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded   = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PULL:8080/PSDSCPullServer.svc'
            RegistrationKey    = 'bbb9778f-43f2-47de-b61e-a0daff474c6d'
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL               = 'http://CONTOSO-REPORT:8080/PSDSCPullServer.svc'
            RegistrationKey         = 'ba39daaa-96c5-4f2f-9149-f95c46460faa'
            AllowUnsecureConnection = $true
        }
    }
}

ReportClientConfig
```

<span data-ttu-id="906ba-119">Следующая конфигурация настраивает узел для использования одного и того же сервера для конфигурации, ресурсов и отчетов.</span><span class="sxs-lookup"><span data-stu-id="906ba-119">The following configuration configures a node to use a single server for configurations, resources, and reporting.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }



        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfig
```

> [!NOTE]
> <span data-ttu-id="906ba-120">При настройке опрашивающего сервера можно указать любое имя веб-службы, но свойство **ServerURL** должно соответствовать имени службы.</span><span class="sxs-lookup"><span data-stu-id="906ba-120">You can name the web service whatever you want when you set up a pull server, but the **ServerURL** property must match the service name.</span></span>

## <a name="getting-report-data"></a><span data-ttu-id="906ba-121">Получение данных из отчетов</span><span class="sxs-lookup"><span data-stu-id="906ba-121">Getting report data</span></span>

<span data-ttu-id="906ba-122">Отчеты, отправляемые на опрашивающий сервер, добавляются в базу данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="906ba-122">Reports sent to the pull server are entered into a database on the server.</span></span> <span data-ttu-id="906ba-123">Отчеты доступны путем вызовов веб-службы.</span><span class="sxs-lookup"><span data-stu-id="906ba-123">The reports are available through calls to the web service.</span></span> <span data-ttu-id="906ba-124">Чтобы извлечь отчеты для конкретного узла, отправьте HTTP-запрос в веб-службу отчетов в следующем формате: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span><span class="sxs-lookup"><span data-stu-id="906ba-124">To retrieve reports for a specific node, send an HTTP request to the report web service in the following form: `http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentId='MyNodeAgentId')/Reports`</span></span>
<span data-ttu-id="906ba-125">где `MyNodeAgentId` — это AgentId узла, с которого вы хотите получать отчеты.</span><span class="sxs-lookup"><span data-stu-id="906ba-125">where `MyNodeAgentId` is the AgentId of the node for which you want to get reports.</span></span> <span data-ttu-id="906ba-126">Вы можете получить AgentID узла, вызвав [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) на этом узле.</span><span class="sxs-lookup"><span data-stu-id="906ba-126">You can get the AgentID for a node by calling [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) on that node.</span></span>

<span data-ttu-id="906ba-127">Отчеты возвращаются в виде массива объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="906ba-127">The reports are returned as an array of JSON objects.</span></span>

<span data-ttu-id="906ba-128">Следующий сценарий возвращает отчеты для узла, на котором он выполняется:</span><span class="sxs-lookup"><span data-stu-id="906ba-128">The following script returns the reports for the node on which it is run:</span></span>

```powershell
function GetReport
{
    param
    (
        $AgentId = "$((glcm).AgentId)", 
        $serviceURL = "http://CONTOSO-REPORT:8080/PSDSCPullServer.svc"
    )

    $requestUri = "$serviceURL/Nodes(AgentId= '$AgentId')/Reports"
    $request = Invoke-WebRequest -Uri $requestUri  -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" `
               -UseBasicParsing -Headers @{Accept = "application/json";ProtocolVersion = "2.0"} `
               -ErrorAction SilentlyContinue -ErrorVariable ev
    $object = ConvertFrom-Json $request.content
    return $object.value
}
```

## <a name="viewing-report-data"></a><span data-ttu-id="906ba-129">Просмотр данных из отчетов</span><span class="sxs-lookup"><span data-stu-id="906ba-129">Viewing report data</span></span>

<span data-ttu-id="906ba-130">Если задать для переменной результат функции **GetReport**, можно просмотреть отдельные поля в элементе возвращаемого массива:</span><span class="sxs-lookup"><span data-stu-id="906ba-130">If you set a variable to the result of the **GetReport** function, you can view the individual fields in an element of the array that is returned:</span></span>

```powershell
$reports = GetReport
$reports[1]
```

```output
JobId                : 019dfbe5-f99f-11e5-80c6-001dd8b8065c
OperationType        : Consistency
RefreshMode          : Pull
Status               : Success
ReportFormatVersion  : 2.0
ConfigurationVersion : 2.0.0
StartTime            : 04/03/2016 06:21:43
EndTime              : 04/03/2016 06:22:04
RebootRequested      : False
Errors               : {}
StatusData           : {{"StartDate":"2016-04-03T06:21:43.7220000-07:00","IPV6Addresses":["2001:4898:d8:f2f2:852b:b255:b071:283b","fe80::852b:b255:b071
                       :283b%12","::2000:0:0:0","::1","::2000:0:0:0"],"DurationInSeconds":"21","JobID":"{019DFBE5-F99F-11E5-80C6-001DD8B8065C}","Curren
                       tChecksum":"A7797571CB9C3AF4D74C39A0FDA11DAF33273349E1182385528FFC1E47151F7F","MetaData":"Author: configAuthor; Name:
                       Sample_ArchiveFirewall; Version: 2.0.0; GenerationDate: 04/01/2016 15:23:30; GenerationHost: CONTOSO-PullSrv;","RebootRequested":"False
                       ","Status":"Success","IPV4Addresses":["10.240.179.151","127.0.0.1"],"LCMVersion":"2.0","ResourcesNotInDesiredState":[{"SourceInf
                       o":"C:\\ReportTest\\Sample_xFirewall_AddFirewallRule.ps1::23::9::xFirewall","ModuleName":"xNetworking","DurationInSeconds":"8.785",
                       "InstanceName":"Firewall","StartDate":"2016-04-03T06:21:56.4650000-07:00","ResourceName":"xFirewall","ModuleVersion":"2.7.0.0","
                       RebootRequested":"False","ResourceId":"[xFirewall]Firewall","ConfigurationName":"Sample_ArchiveFirewall","InDesiredState":"False
                       "}],"NumberOfResources":"2","Type":"Consistency","HostName":"CONTOSO-PULLCLI","ResourcesInDesiredState":[{"SourceInfo":"C:\\ReportTest\\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive","ModuleName":"PSDesiredStateConfiguration","DurationInSeconds":"1.848",
                       "InstanceName":"ArchiveExample","StartDate":"2016-04-03T06:21:56.4650000-07:00","ResourceName":"Archive","ModuleVersion":"1.1","
                       RebootRequested":"False","ResourceId":"[Archive]ArchiveExample","ConfigurationName":"Sample_ArchiveFirewall","InDesiredState":"T
                       rue"}],"MACAddresses":["00-1D-D8-B8-06-5C","00-00-00-00-00-00-00-E0"],"MetaConfiguration":{"AgentId":"52DA826D-00DE-4166-8ACB-73F2B46A7E00",
                       "ConfigurationDownloadManagers":[{"SourceInfo":"C:\\ReportTest\\LCMConfig.ps1::14::9::ConfigurationRepositoryWeb","A
                       llowUnsecureConnection":"True","ServerURL":"http://CONTOSO-PullSrv:8080/PSDSCPullServer.svc","RegistrationKey":"","ResourceId":"[Config
                       urationRepositoryWeb]CONTOSO-PullSrv","ConfigurationNames":["ClientConfig"]}],"ActionAfterReboot":"ContinueConfiguration","LCMCo
                       mpatibleVersions":["1.0","2.0"],"LCMState":"Idle","ResourceModuleManagers":[],"ReportManagers":[{"AllowUnsecureConnection":"True
                       ","RegistrationKey":"","ServerURL":"http://CONTOSO-PullSrv:8080/PSDSCPullServer.svc","ResourceId":"[ReportServerWeb]CONTOSO-PullSrv","S
                       ourceInfo":"C:\\ReportTest\\LCMConfig.ps1::24::9::ReportServerWeb"}],"StatusRetentionTimeInDays":"10","LCMVersion":"2.0","Config
                       urationMode":"ApplyAndMonitor","RefreshFrequencyMins":"30","RebootNodeIfNeeded":"True","RefreshMode":"Pull","DebugMode":["NONE"]
                       ,"LCMStateDetail":"","AllowModuleOverwrite":"False","ConfigurationModeFrequencyMins":"15"},"Locale":"en-US","Mode":"Pull"}}
AdditionalData       : {}
```

<span data-ttu-id="906ba-131">По умолчанию отчеты сортируются по **JobID**.</span><span class="sxs-lookup"><span data-stu-id="906ba-131">By default, the reports are sorted by **JobID**.</span></span> <span data-ttu-id="906ba-132">Чтобы получить последний отчет, отчеты можно отсортировать по убыванию значения свойства **StartTime**, а затем возвратить первый элемент массива:</span><span class="sxs-lookup"><span data-stu-id="906ba-132">To get the most recent report, you can sort the reports by descending **StartTime** property, and then get the first element of the array:</span></span>

```powershell
$reportsByStartTime = $reports | Sort-Object {$_."StartTime" -as [DateTime] } -Descending
$reportMostRecent = $reportsByStartTime[0]
```

<span data-ttu-id="906ba-133">Обратите внимание, что свойство **StatusData** является объектом с несколькими свойствами.</span><span class="sxs-lookup"><span data-stu-id="906ba-133">Notice that the **StatusData** property is an object with a number of properties.</span></span> <span data-ttu-id="906ba-134">Именно здесь находится значительная часть данных отчетов.</span><span class="sxs-lookup"><span data-stu-id="906ba-134">This is where much of the reporting data is.</span></span> <span data-ttu-id="906ba-135">Давайте рассмотрим отдельные поля свойства **StatusData** для последнего отчета.</span><span class="sxs-lookup"><span data-stu-id="906ba-135">Let's look at the individual fields of the **StatusData** property for the most recent report:</span></span>

```powershell
$statusData = $reportMostRecent.StatusData | ConvertFrom-Json
$statusData
```

```output
StartDate                  : 2016-04-04T11:21:41.2990000-07:00
IPV6Addresses              : {2001:4898:d8:f2f2:852b:b255:b071:283b, fe80::852b:b255:b071:283b%12, ::2000:0:0:0, ::1...}
DurationInSeconds          : 25
JobID                      : {135D230E-FA92-11E5-80C6-001DD8B8065C}
CurrentChecksum            : A7797571CB9C3AF4D74C39A0FDA11DAF33273349E1182385528FFC1E47151F7F
MetaData                   : Author: configAuthor; Name: Sample_ArchiveFirewall; Version: 2.0.0; GenerationDate: 04/01/2016 15:23:30; GenerationHost:
                             CONTOSO-PullSrv;
RebootRequested            : False
Status                     : Success
IPV4Addresses              : {10.240.179.151, 127.0.0.1}
LCMVersion                 : 2.0
ResourcesNotInDesiredState : {@{SourceInfo=C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::23::9::xFirewall; ModuleName=xNetworking;
                             DurationInSeconds=10.725; InstanceName=Firewall; StartDate=2016-04-04T11:21:55.7200000-07:00; ResourceName=xFirewall;
                             ModuleVersion=2.7.0.0; RebootRequested=False; ResourceId=[xFirewall]Firewall; ConfigurationName=Sample_ArchiveFirewall;
                             InDesiredState=False}}
NumberOfResources          : 2
Type                       : Consistency
HostName                   : CONTOSO-PULLCLI
ResourcesInDesiredState    : {@{SourceInfo=C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive; ModuleName=PSDesiredStateConfiguration;
                             DurationInSeconds=2.672; InstanceName=ArchiveExample; StartDate=2016-04-04T11:21:55.7200000-07:00; ResourceName=Archive;
                             ModuleVersion=1.1; RebootRequested=False; ResourceId=[Archive]ArchiveExample; ConfigurationName=Sample_ArchiveFirewall;
                             InDesiredState=True}}
MACAddresses               : {00-1D-D8-B8-06-5C, 00-00-00-00-00-00-00-E0}
MetaConfiguration          : @{AgentId=52DA826D-00DE-4166-8ACB-73F2B46A7E00; ConfigurationDownloadManagers=System.Object[];
                             ActionAfterReboot=ContinueConfiguration; LCMCompatibleVersions=System.Object[]; LCMState=Idle;
                             ResourceModuleManagers=System.Object[]; ReportManagers=System.Object[]; StatusRetentionTimeInDays=10; LCMVersion=2.0;
                             ConfigurationMode=ApplyAndMonitor; RefreshFrequencyMins=30; RebootNodeIfNeeded=True; RefreshMode=Pull;
                             DebugMode=System.Object[]; LCMStateDetail=; AllowModuleOverwrite=False; ConfigurationModeFrequencyMins=15}
Locale                     : en-US
Mode                       : Pull
```

<span data-ttu-id="906ba-136">Помимо прочего видно, что последняя конфигурация вызывала два ресурса и один из них был в нужном состоянии, а другой — нет.</span><span class="sxs-lookup"><span data-stu-id="906ba-136">Among other things, this shows that the most recent configuration called two resources, and that one of them was in the desired state, and one of them was not.</span></span> <span data-ttu-id="906ba-137">Вы можете получить более понятные выходные данные только для свойства **ResourcesNotInDesiredState**.</span><span class="sxs-lookup"><span data-stu-id="906ba-137">You can get a more readable output of just the **ResourcesNotInDesiredState** property:</span></span>

```powershell
$statusData.ResourcesInDesiredState
```

```output
SourceInfo        : C:\ReportTest\Sample_xFirewall_AddFirewallRule.ps1::16::9::Archive
ModuleName        : PSDesiredStateConfiguration
DurationInSeconds : 2.672
InstanceName      : ArchiveExample
StartDate         : 2016-04-04T11:21:55.7200000-07:00
ResourceName      : Archive
ModuleVersion     : 1.1
RebootRequested   : False
ResourceId        : [Archive]ArchiveExample
ConfigurationName : Sample_ArchiveFirewall
InDesiredState    : True
```

<span data-ttu-id="906ba-138">Обратите внимание, что эти примеры призваны дать представление о том, что вы можете сделать с данными из отчетов.</span><span class="sxs-lookup"><span data-stu-id="906ba-138">Note that these examples are meant to give you an idea of what you can do with report data.</span></span> <span data-ttu-id="906ba-139">Общие сведения о работе с JSON в PowerShell см. в разделе [Работа с JSON и PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="906ba-139">For an introduction on working with JSON in PowerShell, see [Playing with JSON and PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).</span></span>

## <a name="see-also"></a><span data-ttu-id="906ba-140">См. также</span><span class="sxs-lookup"><span data-stu-id="906ba-140">See Also</span></span>

[<span data-ttu-id="906ba-141">Настройка локального диспетчера конфигураций</span><span class="sxs-lookup"><span data-stu-id="906ba-141">Configuring the Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="906ba-142">Настройка опрашивающего веб-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="906ba-142">Setting up a DSC web pull server</span></span>](pullServer.md)

[<span data-ttu-id="906ba-143">Настройка опрашивающего клиента с помощью имени конфигурации</span><span class="sxs-lookup"><span data-stu-id="906ba-143">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
