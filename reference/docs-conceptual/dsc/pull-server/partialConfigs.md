---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Частичные конфигурации службы настройки требуемого состояния PowerShell
ms.openlocfilehash: 842acad221d468ca5e4c9e660f0205c567bcc220
ms.sourcegitcommit: 30ccbbb32915b551c4cd4c91ef1df96b5b7514c4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/01/2020
ms.locfileid: "80500771"
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a><span data-ttu-id="a3033-103">Частичные конфигурации службы настройки требуемого состояния PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3033-103">PowerShell Desired State Configuration partial configurations</span></span>

<span data-ttu-id="a3033-104">_Применяется к: Windows PowerShell 5.0 и последующих версий._</span><span class="sxs-lookup"><span data-stu-id="a3033-104">_Applies To: Windows PowerShell 5.0 and later._</span></span>

<span data-ttu-id="a3033-105">В PowerShell 5.0 служба настройки требуемого состояния (DSC) разрешает доставлять конфигурации фрагментами и из нескольких источников.</span><span class="sxs-lookup"><span data-stu-id="a3033-105">In PowerShell 5.0, Desired State Configuration (DSC) allows configurations to be delivered in fragments and from multiple sources.</span></span> <span data-ttu-id="a3033-106">Локальный диспетчер конфигураций (LCM) на целевом узле объединяет фрагменты перед тем, как применить их в качестве единой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3033-106">The Local Configuration Manager (LCM) on the target node puts the fragments together before applying them as a single configuration.</span></span> <span data-ttu-id="a3033-107">Эта возможность позволяет разделять конфигурацию между командами или отдельными пользователями.</span><span class="sxs-lookup"><span data-stu-id="a3033-107">This capability allows sharing control of configuration between teams or individuals.</span></span> <span data-ttu-id="a3033-108">Например, если несколько команд разработчиков совместно работают над службой, возможно, каждая из них хочет создать конфигурацию для управления своей частью службы.</span><span class="sxs-lookup"><span data-stu-id="a3033-108">For example, if two or more teams of developers are collaborating on a service, they might each want to create configurations to manage their part of the service.</span></span> <span data-ttu-id="a3033-109">Каждую из этих конфигураций можно извлекать с разных опрашивающих серверов и добавлять на разных этапах разработки.</span><span class="sxs-lookup"><span data-stu-id="a3033-109">Each of these configurations could be pulled from different pull servers, and they could be added at different stages of development.</span></span> <span data-ttu-id="a3033-110">Частичные конфигурации позволяют разным пользователям или командам контролировать различные аспекты настройки узлов без координации изменений в едином документе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3033-110">Partial configurations also allow different individuals or teams to control different aspects of configuring nodes without having to coordinate the editing of a single configuration document.</span></span> <span data-ttu-id="a3033-111">Например, одна команда может отвечать за развертывание виртуальной машины и операционной системы, тогда как другая — развертывать другие приложения и службы в этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a3033-111">For example, one team might be responsible for deploying a VM and operating system, while another team might deploy other applications and services on that VM.</span></span> <span data-ttu-id="a3033-112">С частичными конфигурациями каждая команда может создать собственную конфигурацию без излишних сложностей.</span><span class="sxs-lookup"><span data-stu-id="a3033-112">With partial configurations, each team can create its own configuration, without either of them being unnecessarily complicated.</span></span>

<span data-ttu-id="a3033-113">Вы можете использовать частичные конфигурации в режиме принудительной отправки, в режиме запроса или в сочетании.</span><span class="sxs-lookup"><span data-stu-id="a3033-113">You can use partial configurations in push mode, pull mode, or a combination of the two.</span></span>

## <a name="partial-configurations-in-push-mode"></a><span data-ttu-id="a3033-114">Частичные конфигурации в режиме принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="a3033-114">Partial configurations in push mode</span></span>

<span data-ttu-id="a3033-115">Чтобы использовать частичные конфигурации в режиме принудительной отправки, настройте LCM на целевом узле для получения частичных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="a3033-115">To use partial configurations in push mode, you configure the LCM on the target node to receive the partial configurations.</span></span> <span data-ttu-id="a3033-116">Каждая частичная конфигурация должна принудительно отправляться на целевой узел с использованием командлета `Publish-DSCConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="a3033-116">Each partial configuration must be pushed to the target by using the `Publish-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="a3033-117">Затем целевой узел добавляет частичную конфигурацию в единую. Применить конфигурацию можно, вызвав командлет [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration).</span><span class="sxs-lookup"><span data-stu-id="a3033-117">The target node then combines the partial configuration into a single configuration, and you can apply the configuration by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a><span data-ttu-id="a3033-118">Настройка LCM для частичных конфигураций в режиме принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="a3033-118">Configuring the LCM for push-mode partial configurations</span></span>

<span data-ttu-id="a3033-119">Чтобы настроить LCM для частичных конфигураций в режиме принудительной отправки, создайте конфигурацию **DSCLocalConfigurationManager** с одним блоком **PartialConfiguration** для каждой частичной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3033-119">To configure the LCM for partial configurations in push mode, you create a **DSCLocalConfigurationManager** configuration with one **PartialConfiguration** block for each partial configuration.</span></span> <span data-ttu-id="a3033-120">Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций в Windows](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="a3033-120">For more information about configuring the LCM, see [Windows Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span> <span data-ttu-id="a3033-121">В следующем примере показана конфигурация LCM, в которой ожидаются две частичные конфигурации: та, которая развертывает ОС, и та, которая развертывает и настраивает SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a3033-121">The following example shows an LCM configuration that expects two partial configurations—one that deploys the OS, and one that deploys and configures SharePoint.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {

        PartialConfiguration ServiceAccountConfig
        {
            Description = 'Configuration to add the SharePoint service account to the Administrators group.'
            RefreshMode = 'Push'
        }
           PartialConfiguration SharePointConfig
        {
            Description = 'Configuration for the SharePoint server'
            RefreshMode = 'Push'
        }
    }
}

PartialConfigDemo
```

<span data-ttu-id="a3033-122">**RefreshMode** для каждой частичной конфигурации имеет значение Push.</span><span class="sxs-lookup"><span data-stu-id="a3033-122">The **RefreshMode** for each partial configuration is set to "Push".</span></span> <span data-ttu-id="a3033-123">Имена блоков **PartialConfiguration** (в этом случае ServiceAccountConfig и SharePointConfig) должны точно совпадать с именами конфигураций, отправляемых на целевой узел.</span><span class="sxs-lookup"><span data-stu-id="a3033-123">The names of the **PartialConfiguration** blocks (in this case, "ServiceAccountConfig" and "SharePointConfig") must match exactly the names of the configurations that are pushed to the target node.</span></span>

> [!Note]
> <span data-ttu-id="a3033-124">Название каждого блока **PartialConfiguration** должно совпадать с фактическим названием конфигурации (которое указано в сценарии конфигурации), а не с именем MOF-файла, которое должно быть названием целевого узла или `localhost`.</span><span class="sxs-lookup"><span data-stu-id="a3033-124">The named of each **PartialConfiguration** block must match the actual name of the configuration as it is specified in the configuration script, not the name of the MOF file, which should be either the name of the target node or `localhost`.</span></span>

### <a name="publishing-and-starting-push-mode-partial-configurations"></a><span data-ttu-id="a3033-125">Публикация и запуск частичных конфигураций в режиме принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="a3033-125">Publishing and starting push-mode partial configurations</span></span>

<span data-ttu-id="a3033-126">Затем вызовите [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) для каждой конфигурации, передав папки с документами конфигурации, в качестве параметров **Path**.</span><span class="sxs-lookup"><span data-stu-id="a3033-126">You then call [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) for each configuration, passing the folders that contain the configuration documents as the **Path** parameters.</span></span> <span data-ttu-id="a3033-127">`Publish-DSCConfiguration` помещает конфигурацию MOF-файлов на целевые узлы.</span><span class="sxs-lookup"><span data-stu-id="a3033-127">`Publish-DSCConfiguration`places the configuration MOF files to the target nodes.</span></span> <span data-ttu-id="a3033-128">После публикации обеих конфигураций вы можете вызвать `Start-DSCConfiguration –UseExisting` на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="a3033-128">After publishing both configurations, you can call `Start-DSCConfiguration –UseExisting` on the target node.</span></span>

<span data-ttu-id="a3033-129">Например, если вы скомпилировали следующую конфигурацию документов MOF на узле разработки:</span><span class="sxs-lookup"><span data-stu-id="a3033-129">For example, if you have compiled the following configuration MOF documents on the authoring node:</span></span>

```powershell
Get-ChildItem -Recurse
```

```output
    Directory: C:\PartialConfigTest

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        8/11/2016   1:55 PM                ServiceAccountConfig
d-----       11/17/2016   4:14 PM                SharePointConfig

    Directory: C:\PartialConfigTest\ServiceAccountConfig

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        8/11/2016   2:02 PM           2034 TestVM.mof

    Directory: C:\PartialConfigTest\SharePointConfig

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       11/17/2016   4:14 PM           1930 TestVM.mof
```

<span data-ttu-id="a3033-130">Публикация и запуск конфигураций выполняются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3033-130">You would publish and run the configurations as follows:</span></span>

```powershell
Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
Start-DscConfiguration -UseExisting -ComputerName 'TestVM'
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

> [!Note]
> <span data-ttu-id="a3033-131">Пользователь, запускающий командлет [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration), должен иметь права администратора на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="a3033-131">The user running the [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) cmdlet must have administrator privileges on the target node.</span></span>

## <a name="partial-configurations-in-pull-mode"></a><span data-ttu-id="a3033-132">Частичные конфигурации в режиме запросов</span><span class="sxs-lookup"><span data-stu-id="a3033-132">Partial configurations in pull mode</span></span>

<span data-ttu-id="a3033-133">Частичные конфигурации можно запросить из одного или нескольких опрашивающих серверов (дополнительные сведения об опрашивающих серверах см. в разделе [Опрашивающие сервера настройки требуемого состояния Windows PowerShell](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="a3033-133">Partial configurations can be pulled from one or more pull servers (for more information about pull servers, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="a3033-134">Для этого необходимо настроить в LCM на целевом узле извлечение частичных конфигураций, а также назвать документы конфигурации и указать их расположение на опрашивающих серверах.</span><span class="sxs-lookup"><span data-stu-id="a3033-134">To do this, you have to configure the LCM on the target node to pull the partial configurations, and name and locate the configuration documents properly on the pull servers.</span></span>

### <a name="configuring-the-lcm-for-pull-node-configurations"></a><span data-ttu-id="a3033-135">Настройка LCM для конфигураций опрашивающего узла</span><span class="sxs-lookup"><span data-stu-id="a3033-135">Configuring the LCM for pull node configurations</span></span>

<span data-ttu-id="a3033-136">Чтобы настроить в LCM опрос частичных конфигураций с опрашивающего сервера, определите опрашивающий сервер в блоке **ConfigurationRepositoryWeb** (для опрашивающего HTTP-сервера) или **ConfigurationRepositoryShare** (для опрашивающего SMB-сервера).</span><span class="sxs-lookup"><span data-stu-id="a3033-136">To configure the LCM to pull partial configurations from a pull server, you define the pull server in either a **ConfigurationRepositoryWeb** (for an HTTP pull server) or **ConfigurationRepositoryShare** (for an SMB pull server) block.</span></span> <span data-ttu-id="a3033-137">Затем создайте блоки **PartialConfiguration**, которые ссылаются на опрашивающий сервер, используя свойство **ConfigurationSource**.</span><span class="sxs-lookup"><span data-stu-id="a3033-137">You then create **PartialConfiguration** blocks that refer to the pull server by using the **ConfigurationSource** property.</span></span> <span data-ttu-id="a3033-138">Кроме того, вам потребуется создать блок **параметров**, чтобы указать, что LCM использует режим запросов, и задать **ConfigurationNames** или **ConfigurationID** для опрашивающего сервера и целевого узла в целях определения конфигураций.</span><span class="sxs-lookup"><span data-stu-id="a3033-138">You also need to create a **Settings** block to specify that the LCM uses pull mode, and to specify the **ConfigurationNames** or **ConfigurationID** that the pull server and target node use to identify the configurations.</span></span> <span data-ttu-id="a3033-139">В следующей метаконфигурации задан опрашивающий HTTP-сервер с именем CONTOSO-PullSrv и две частичные конфигурации, использующие этот опрашивающий сервер.</span><span class="sxs-lookup"><span data-stu-id="a3033-139">The following meta-configuration defines an HTTP pull server named CONTOSO-PullSrv and two partial configurations that use that pull server.</span></span>

<span data-ttu-id="a3033-140">Дополнительные сведения о настройке LCM с использованием **ConfigurationNames** см. в разделе [Настройка опрашивающего клиента с помощью имен конфигурации](pullClientConfigNames.md).</span><span class="sxs-lookup"><span data-stu-id="a3033-140">For more information about configuring the LCM using **ConfigurationNames**, see [Setting up a pull client using configuration names](pullClientConfigNames.md).</span></span> <span data-ttu-id="a3033-141">Дополнительные сведения о настройке LCM с использованием **ConfigurationID** см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="a3033-141">For information about configuring the LCM using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a><span data-ttu-id="a3033-142">Настройка LCM для конфигураций режима запросов с использованием имен конфигурации</span><span class="sxs-lookup"><span data-stu-id="a3033-142">Configuring the LCM for pull mode configurations using configuration names</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               ="ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
        }
}
```

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a><span data-ttu-id="a3033-143">Настройка LCM для конфигураций режима запросов с использованием ConfigurationID</span><span class="sxs-lookup"><span data-stu-id="a3033-143">Configuring the LCM for pull mode configurations using ConfigurationID</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemoConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode                     = 'Pull'
            ConfigurationID                 = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins            = 30
            RebootNodeIfNeeded              = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description                     = 'Configuration for the Base OS'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode                     = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description                     = 'Configuration for the Sharepoint Server'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Pull'
        }
    }
}
PartialConfigDemo
```

<span data-ttu-id="a3033-144">Вы можете извлечь частичные конфигурации более чем из одного опрашивающего сервера — потребуется только определить каждый опрашивающий сервер, а затем сослаться на соответствующий опрашивающий сервер в каждом блоке **PartialConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="a3033-144">You can pull partial configurations from more than one pull server—you would just need to define each pull server, and then refer to the appropriate pull server in each **PartialConfiguration** block.</span></span>

<span data-ttu-id="a3033-145">После создания метаконфигурации необходимо запустить ее для создания документа конфигурации (MOF-файла), а затем вызвать [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) для настройки LCM.</span><span class="sxs-lookup"><span data-stu-id="a3033-145">After creating the meta-configuration, you must run it to create a configuration document (a MOF file), and then call [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) to configure the LCM.</span></span>

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a><span data-ttu-id="a3033-146">Именование и размещение документов конфигурации на опрашивающем сервере (ConfigurationNames)</span><span class="sxs-lookup"><span data-stu-id="a3033-146">Naming and placing the configuration documents on the pull server (ConfigurationNames)</span></span>

<span data-ttu-id="a3033-147">Документы частичной конфигурации необходимо разместить в папке, указанной как **ConfigurationPath**, в файле `web.config` для опрашивающего сервера (обычно `C:\Program
Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="a3033-147">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program
Files\WindowsPowerShell\DscService\Configuration`).</span></span>

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a><span data-ttu-id="a3033-148">Именование документов конфигурации на опрашивающем сервере в PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="a3033-148">Naming configuration documents on the pull server in PowerShell 5.1</span></span>

<span data-ttu-id="a3033-149">Если вы запрашиваете только одну частичную конфигурацию на отдельном опрашивающем сервере, документ конфигурации может иметь любое имя.</span><span class="sxs-lookup"><span data-stu-id="a3033-149">If you are pulling only one partial configuration from an individual pull server, the configuration document can have any name.</span></span> <span data-ttu-id="a3033-150">Если вы запрашиваете с опрашивающего сервера несколько частичных конфигураций, документ конфигурации можно назвать `<ConfigurationName>.mof`, где *ConfigurationName* — имя частичной конфигурации, или `<ConfigurationName>.<NodeName>.mof`, где *ConfigurationName* — имя частичной конфигурации, а *NodeName* — имя целевого узла.</span><span class="sxs-lookup"><span data-stu-id="a3033-150">If you are pulling more than one partial configuration from a pull server, the configuration document can be named either `<ConfigurationName>.mof`, where *ConfigurationName* is the name of the partial configuration, or `<ConfigurationName>.<NodeName>.mof`, where *ConfigurationName* is the name of the partial configuration, and *NodeName* is the name of the target node.</span></span> <span data-ttu-id="a3033-151">Это позволяет запрашивать конфигурации с опрашивающего сервера DSC службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="a3033-151">This allows you to pull configurations from Azure Automation DSC pull server.</span></span>

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a><span data-ttu-id="a3033-152">Именование документов конфигурации на опрашивающем сервере в PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a3033-152">Naming configuration documents on the pull server in PowerShell 5.0</span></span>

<span data-ttu-id="a3033-153">Документы конфигурации должны быть именованы следующим образом: `ConfigurationName.mof`, где *ConfigurationName* — имя частичной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3033-153">The configuration documents must be named as follows: `ConfigurationName.mof`, where *ConfigurationName* is the name of the partial configuration.</span></span> <span data-ttu-id="a3033-154">Например, документы конфигурации следует назвать следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a3033-154">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a><span data-ttu-id="a3033-155">Именование и размещение документов конфигурации на опрашивающем сервере (ConfigurationID)</span><span class="sxs-lookup"><span data-stu-id="a3033-155">Naming and placing the configuration documents on the pull server (ConfigurationID)</span></span>

<span data-ttu-id="a3033-156">Документы частичной конфигурации необходимо разместить в папке, указанной как **ConfigurationPath**, в файле `web.config` для опрашивающего сервера (обычно `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="a3033-156">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> <span data-ttu-id="a3033-157">Документы конфигурации должны называться так: `<ConfigurationName>.<ConfigurationID>.mof`, где _ConfigurationName_ — имя частичной конфигурации, а _ConfigurationID_ — идентификатор конфигурации, заданным в LCM на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="a3033-157">The configuration documents must be named as follows: `<ConfigurationName>.<ConfigurationID>.mof`, where _ConfigurationName_ is the name of the partial configuration and _ConfigurationID_ is the configuration ID defined in the LCM on the target node.</span></span> <span data-ttu-id="a3033-158">Например, документы конфигурации следует назвать следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a3033-158">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```

### <a name="running-partial-configurations-from-a-pull-server"></a><span data-ttu-id="a3033-159">Запуск частичных конфигураций с опрашивающего сервера</span><span class="sxs-lookup"><span data-stu-id="a3033-159">Running partial configurations from a pull server</span></span>

<span data-ttu-id="a3033-160">После настройки LCM на целевом узле, а также создания и именования документов на опрашивающем сервере целевой узел запросит частичные конфигурации, объединит их и будет применять результирующую конфигурацию с регулярными интервалами, указанными свойством **RefreshFrequencyMins** в LCM.</span><span class="sxs-lookup"><span data-stu-id="a3033-160">After the LCM on the target node has been configured, and the configuration documents have been created and properly named on the pull server, the target node will pull the partial configurations, combine them, and apply the resulting configuration at regular intervals as specified by the **RefreshFrequencyMins** property of the LCM.</span></span> <span data-ttu-id="a3033-161">Если вы хотите принудительно применить обновление, можно вызвать командлет [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) для извлечения конфигураций, а затем `Start-DSCConfiguration –UseExisting` для их применения.</span><span class="sxs-lookup"><span data-stu-id="a3033-161">If you want to force a refresh, you can call the [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) cmdlet, to pull the configurations, and then `Start-DSCConfiguration –UseExisting` to apply them.</span></span>

## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a><span data-ttu-id="a3033-162">Частичные конфигурации в смешанных режимах принудительной отправки и запросов</span><span class="sxs-lookup"><span data-stu-id="a3033-162">Partial configurations in mixed push and pull modes</span></span>

<span data-ttu-id="a3033-163">Кроме того, вы можете совместить режимы принудительной отправки и запросов для частичных конфигураций</span><span class="sxs-lookup"><span data-stu-id="a3033-163">You can also mix push and pull modes for partial configurations.</span></span> <span data-ttu-id="a3033-164">Это значит, что у вас может быть одна частичная конфигурация, запрашиваемая с опрашивающего сервера, тогда как для другой частичной конфигурации выполняется принудительная отправка.</span><span class="sxs-lookup"><span data-stu-id="a3033-164">That is, you could have one partial configuration that is pulled from a pull server, while another partial configuration is pushed.</span></span> <span data-ttu-id="a3033-165">Укажите режим обновления для каждой частичной конфигурации, как описано в предыдущих разделах.</span><span class="sxs-lookup"><span data-stu-id="a3033-165">Specify the refresh mode for each partial configuration as described in the previous sections.</span></span> <span data-ttu-id="a3033-166">Например, в следующей метаконфигурации описывается один и тот же пример с частичной конфигурацией `ServiceAccountConfig` в режиме запросов и частичной конфигурацией `SharePointConfig` в режиме принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="a3033-166">For example, the following meta-configuration describes the same example, with the `ServiceAccountConfig` partial configuration in pull mode and the `SharePointConfig` partial configuration in push mode.</span></span>

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a><span data-ttu-id="a3033-167">Смешанные режимы принудительной отправки и запросов с использованием ConfigurationNames</span><span class="sxs-lookup"><span data-stu-id="a3033-167">Mixed push and pull modes using ConfigurationNames</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               = "ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            RefreshMode                     = 'Pull'
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Push'
        }

}
```

### <a name="mixed-push-and-pull-modes-using-configurationid"></a><span data-ttu-id="a3033-168">Смешанные режимы принудительной отправки и запросов с использованием ConfigurationID</span><span class="sxs-lookup"><span data-stu-id="a3033-168">Mixed push and pull modes using ConfigurationID</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {
        Settings
        {
            RefreshMode             = 'Pull'
            ConfigurationID         = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins    = 30
            RebootNodeIfNeeded      = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL               = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description             = 'Configuration for the Base OS'
            ConfigurationSource     = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode             = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description             = 'Configuration for the Sharepoint Server'
            DependsOn               = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode             = 'Push'
        }
    }
}
PartialConfigDemo
```

<span data-ttu-id="a3033-169">Обратите внимание, что режим **RefreshMode**, указанный в блоке "Параметры", — это "Режим запросов", а режим **RefreshMode** для частичной конфигурации `SharePointConfig` — "Режим принудительной отправки".</span><span class="sxs-lookup"><span data-stu-id="a3033-169">Note that the **RefreshMode** specified in the Settings block is "Pull", but the **RefreshMode** for the `SharePointConfig` partial configuration is "Push".</span></span>

<span data-ttu-id="a3033-170">MOF-файлы конфигурации следует именовать и располагать в соответствии с их режимами обновления.</span><span class="sxs-lookup"><span data-stu-id="a3033-170">Name and locate the configuration MOF files as described above for their respective refresh modes.</span></span>
<span data-ttu-id="a3033-171">Вызовите `Publish-DSCConfiguration`, чтобы опубликовать частичную конфигурацию `SharePointConfig`, и дождитесь извлечения конфигурации `ServiceAccountConfig` из опрашивающего сервера или выполните принудительное обновление, вызвав [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).</span><span class="sxs-lookup"><span data-stu-id="a3033-171">Call `Publish-DSCConfiguration` to publish the `SharePointConfig` partial configuration, and either wait for the `ServiceAccountConfig` configuration to be pulled from the pull server, or force a refresh by calling [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).</span></span>

## <a name="example-serviceaccountconfig-partial-configuration"></a><span data-ttu-id="a3033-172">Пример частичной конфигурации ServiceAccountConfig</span><span class="sxs-lookup"><span data-stu-id="a3033-172">Example ServiceAccountConfig Partial Configuration</span></span>

```powershell
Configuration ServiceAccountConfig
{
    Param (
        [Parameter(Mandatory,
                   HelpMessage="Domain credentials required to add domain\sharepoint_svc to the local Administrators group.")]
        [ValidateNotNullOrEmpty()]
        [pscredential]$Credential
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Group LocalAdmins
        {
            GroupName           = 'Administrators'
            MembersToInclude    = 'domain\sharepoint_svc',
                                  'admins@example.domain'
            Ensure              = 'Present'
            Credential          = $Credential
        }

        WindowsFeature Telnet
        {
            Name                = 'Telnet-Server'
            Ensure              = 'Absent'
        }
    }
}
ServiceAccountConfig
```

## <a name="example-sharepointconfig-partial-configuration"></a><span data-ttu-id="a3033-173">Пример частичной конфигурации SharePointConfig</span><span class="sxs-lookup"><span data-stu-id="a3033-173">Example SharePointConfig Partial Configuration</span></span>

```powershell
Configuration SharePointConfig
{
    Param (
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [pscredential]$ProductKey
    )

    Import-DscResource -ModuleName xSharePoint

    Node localhost
    {
        xSPInstall SharePointDefault
        {
            Ensure      = 'Present'
            BinaryDir   = '\\FileServer\Installers\Sharepoint\'
            ProductKey  = $ProductKey
        }
    }
}
SharePointConfig
```

## <a name="see-also"></a><span data-ttu-id="a3033-174">См. также:</span><span class="sxs-lookup"><span data-stu-id="a3033-174">See Also</span></span>

[<span data-ttu-id="a3033-175">Опрашивающая служба Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="a3033-175">Windows PowerShell Desired State Configuration Pull Servers</span></span>](pullServer.md)

[<span data-ttu-id="a3033-176">Настройка локального диспетчера конфигураций Windows</span><span class="sxs-lookup"><span data-stu-id="a3033-176">Windows Configuring the Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)
