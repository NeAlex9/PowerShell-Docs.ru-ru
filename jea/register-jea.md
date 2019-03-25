---
ms.date: 06/12/2017
keywords: jea,powershell,безопасность
title: Регистрация конфигураций JEA
ms.openlocfilehash: 6fa0ce434c8e70eb718545e99417bfe034cda6bf
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2019
ms.locfileid: "58059445"
---
# <a name="registering-jea-configurations"></a><span data-ttu-id="1a0ad-103">Регистрация конфигураций JEA</span><span class="sxs-lookup"><span data-stu-id="1a0ad-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="1a0ad-104">Применяется к: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1a0ad-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="1a0ad-105">Последний шаг перед использованием JEA после создания [возможностей роли](role-capabilities.md) и [файла конфигурации сеанса](session-configurations.md) заключается в регистрации конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-105">Once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created, the last step before you can use JEA is to register the JEA endpoint.</span></span>
<span data-ttu-id="1a0ad-106">Регистрация конечной точки JEA в системе делает конечную точку доступной пользователям и модулям автоматизации.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-106">Registering the JEA endpoint with the system makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="1a0ad-107">Конфигурация для отдельного компьютера</span><span class="sxs-lookup"><span data-stu-id="1a0ad-107">Single machine configuration</span></span>

<span data-ttu-id="1a0ad-108">Для небольших сред можно развернуть JEA, зарегистрировав файл конфигурации сеанса с помощью командлета [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="1a0ad-109">Прежде чем приступать к этой процедуре, убедитесь, что выполняются следующие необходимые условия:</span><span class="sxs-lookup"><span data-stu-id="1a0ad-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="1a0ad-110">Создана одна или несколько ролей, которые помещены в папку "RoleCapabilities" для допустимого модуля PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="1a0ad-111">Создан и проверен файл конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="1a0ad-112">Пользователь, регистрирующий конфигурацию JEA, обладает правами администратора в соответствующих системах.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="1a0ad-113">Кроме того, требуется выбрать имя для конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-113">You also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="1a0ad-114">Это имя запрашивается при подключении пользователей к системе с помощью JEA.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-114">The name of the JEA endpoint is required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="1a0ad-115">Для просмотра имен существующих конечных точек в системе можно использовать командлет [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="1a0ad-116">Конечные точки, начинающиеся со слова "microsoft", обычно поставляются с Windows.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="1a0ad-117">Конечная точка "microsoft.powershell" используется по умолчанию при подключении к удаленной конечной точке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="1a0ad-118">После определения имени для конечной точки JEA выполните приведенную ниже команду, чтобы зарегистрировать конечную точку.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="1a0ad-119">Приведенная выше команда перезапускает службу WinRM в системе.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-119">The above command restarts the WinRM service on the system.</span></span>
> <span data-ttu-id="1a0ad-120">При этом завершаются все сеансы удаленного взаимодействия PowerShell, а также любые текущие конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-120">This terminates all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="1a0ad-121">Перед выполнением этой команды рекомендуется перевести рабочие компьютеры в автономный режим, чтобы избежать нарушения бизнес-операции.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="1a0ad-122">Если регистрация прошла успешно, можно приступать к [использованию JEA](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-122">If registration is successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="1a0ad-123">Файл конфигурации сеанса можно удалить в любое время, так как после регистрации конечной точки он не используется.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-123">You may delete the session configuration file at any time; it is not used after registration of the end point.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="1a0ad-124">Конфигурация для нескольких компьютеров с помощью DSC</span><span class="sxs-lookup"><span data-stu-id="1a0ad-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="1a0ad-125">Если JEA развертывается на нескольких компьютерах, самая простая модель развертывания заключается в использовании ресурса [настройки требуемого состояния](https://msdn.microsoft.com/powershell/dsc/overview) JEA, позволяющего быстро и согласованно развернуть JEA на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="1a0ad-126">Чтобы развернуть JEA с помощью DSC, следует убедиться в выполнении следующих условий:</span><span class="sxs-lookup"><span data-stu-id="1a0ad-126">To deploy JEA with DSC, you need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="1a0ad-127">Создана одна или несколько возможностей ролей, которые были добавлены в допустимый модуль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="1a0ad-128">Модуль PowerShell, содержащий нужные роли, хранится в (доступной только для чтения) общей папке, видимой каждому компьютеру.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="1a0ad-129">Были определены параметры для конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="1a0ad-130">При использовании ресурса DSC JEA создавать файл конфигурации сеанса не требуется.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="1a0ad-131">Вы имеете учетные данные, которые позволяют выполнять административные действия на каждом компьютере, или доступ к опрашивающему серверу DSC, используемому для управления компьютерами.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-131">You have credentials that allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="1a0ad-132">Вы загрузили [ресурс DSC JEA](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="1a0ad-133">На целевом компьютере (или опрашивающем сервере, если вы используете его) создайте конфигурацию DSC для конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="1a0ad-134">В этой конфигурации используйте ресурс DSC JustEnoughAdministration для настройки файла конфигурации сеанса и ресурс File для копирования возможностей ролей из общей папки.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-134">In this configuration, you use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="1a0ad-135">С помощью ресурса DSC можно настраивать следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="1a0ad-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="1a0ad-136">Определения ролей</span><span class="sxs-lookup"><span data-stu-id="1a0ad-136">Role Definitions</span></span>
- <span data-ttu-id="1a0ad-137">Группы виртуальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="1a0ad-137">Virtual Account groups</span></span>
- <span data-ttu-id="1a0ad-138">Имя групповой управляемой учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="1a0ad-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="1a0ad-139">Каталог записей</span><span class="sxs-lookup"><span data-stu-id="1a0ad-139">Transcript directory</span></span>
- <span data-ttu-id="1a0ad-140">Диск пользователя</span><span class="sxs-lookup"><span data-stu-id="1a0ad-140">User drive</span></span>
- <span data-ttu-id="1a0ad-141">Правила условного доступа</span><span class="sxs-lookup"><span data-stu-id="1a0ad-141">Conditional access rules</span></span>
- <span data-ttu-id="1a0ad-142">Сценарии запуска для сеанса JEA</span><span class="sxs-lookup"><span data-stu-id="1a0ad-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="1a0ad-143">Синтаксис для каждого из этих свойств в конфигурации DSC согласуется с файлом конфигурации сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="1a0ad-144">Ниже приведен пример конфигурации DSC для модуля общего обслуживания сервера.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="1a0ad-145">Предполагается, что допустимый модуль PowerShell, содержащий возможности ролей во вложенной папке "RoleCapabilities", находится в общей папке "\\\\myfileshare\\JEA".</span><span class="sxs-lookup"><span data-stu-id="1a0ad-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


```powershell
Configuration JEAMaintenance
{
    Import-DscResource -Module JustEnoughAdministration, PSDesiredStateConfiguration

    File MaintenanceModule
    {
        SourcePath = "\\myfileshare\JEA\ContosoMaintenance"
        DestinationPath = "C:\Program Files\WindowsPowerShell\Modules\ContosoMaintenance"
        Checksum = "SHA-256"
        Ensure = "Present"
        Type = "Directory"
        Recurse = $true
    }

    JeaEndpoint JEAMaintenanceEndpoint
    {
        EndpointName = "JEAMaintenance"
        RoleDefinitions = "@{ 'CONTOSO\JEAMaintenanceAuditors' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit' }; 'CONTOSO\JEAMaintenanceAdmins' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit', 'GeneralServerMaintenance-Admin' } }"
        TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
        DependsOn = '[File]MaintenanceModule'
    }
}
```

<span data-ttu-id="1a0ad-146">Затем эту конфигурацию можно применить в системе, [напрямую вызвав локальный диспетчер конфигураций](https://msdn.microsoft.com/powershell/dsc/metaconfig) или обновив [конфигурацию опрашивающего сервера](https://msdn.microsoft.com/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="1a0ad-147">Ресурс DSC также позволяет заменить конечную точку удаленного взаимодействия по умолчанию Microsoft.PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="1a0ad-148">В этом случае ресурс автоматически регистрирует резервную конечную точку без ограничений с именем Microsoft.PowerShell.Restricted, имеющую ACL WinRM по умолчанию (который предоставляет членам групп "Локальные администраторы" и "Пользователи удаленного управления" доступ к ней).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-148">If you do this, the resource automatically registers a backup unconstrained endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="1a0ad-149">Отмена регистрации конфигураций JEA</span><span class="sxs-lookup"><span data-stu-id="1a0ad-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="1a0ad-150">Чтобы удалить конечную точку JEA из системы, используйте командлет [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1a0ad-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="1a0ad-151">Отмена регистрации конечной точки JEA не позволяет новым пользователям создавать новые сеансы JEA в системе.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-151">Unregistering a JEA endpoint prevents new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="1a0ad-152">Кроме того, вы можете обновить конфигурацию JEA, повторно зарегистрировав измененный файл конфигурации сеанса с использованием такого же имени конечной точки.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="1a0ad-153">Отмена регистрации конечной точки JEA вызывает перезапуск службы WinRM.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-153">Unregistering a JEA endpoint causes the WinRM service to restart.</span></span>
> <span data-ttu-id="1a0ad-154">Это приводит к прерыванию большинства выполняемых операций удаленного управления, включая другие сеансы PowerShell, вызовы WMI и некоторые средства управления.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-154">This interrupts most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="1a0ad-155">Отменяйте регистрацию конечных точек PowerShell только во время запланированных периодов обслуживания.</span><span class="sxs-lookup"><span data-stu-id="1a0ad-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a0ad-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a0ad-156">Next steps</span></span>

- [<span data-ttu-id="1a0ad-157">Тестирование конечной точки JEA</span><span class="sxs-lookup"><span data-stu-id="1a0ad-157">Test the JEA endpoint</span></span>](using-jea.md)
