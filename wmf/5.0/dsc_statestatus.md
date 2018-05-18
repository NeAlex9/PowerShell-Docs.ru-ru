---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 272843efb68c42105af6eb88ad6a95b581da47ae
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="56ca2-102">Единое и согласованное представление состояний</span><span class="sxs-lookup"><span data-stu-id="56ca2-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="56ca2-103">В этот выпуск внесен ряд усовершенствований для служб автоматизации, отвечающих за состояние LCM и DSC.</span><span class="sxs-lookup"><span data-stu-id="56ca2-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="56ca2-104">Сюда входят единые и согласованные представления состояния, управляемое свойство datetime объектов состояния, возвращаемых командлетом Get-DscConfigurationStatus, и свойство расширенных сведений о состоянии LCM, возвращаемое командлетом Get-DscLocalConfigurationManager.</span><span class="sxs-lookup"><span data-stu-id="56ca2-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by Get-DscConfigurationStatus cmdlet and enhanced LCM state details property returned by Get-DscLocalConfigurationManager cmdlet.</span></span>

<span data-ttu-id="56ca2-105">Это представление состояния LCM и DSC пересмотрено и унифицировано согласно следующим правилам:</span><span class="sxs-lookup"><span data-stu-id="56ca2-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>
1.  <span data-ttu-id="56ca2-106">Необработанный ресурс не влияет на состояние LCM и DSC.</span><span class="sxs-lookup"><span data-stu-id="56ca2-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2.  <span data-ttu-id="56ca2-107">LCM останавливает обработку дальнейших ресурсов, встретив ресурс, который требует перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="56ca2-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3.  <span data-ttu-id="56ca2-108">Ресурс, требующий перезагрузку, не находится в нужном состоянии до ее фактического выполнения.</span><span class="sxs-lookup"><span data-stu-id="56ca2-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4.  <span data-ttu-id="56ca2-109">После обнаружения ресурса, завершающегося сбоем, LCM продолжает обрабатывать дальнейшие ресурсы, если только они не зависят от ресурса со сбоем.</span><span class="sxs-lookup"><span data-stu-id="56ca2-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5.  <span data-ttu-id="56ca2-110">Общее состояние, возвращаемое командлетом Get-DscConfigurationStatus, представляет собой супермножество состояния для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="56ca2-110">The overall status returned by Get-DscConfigurationStatus cmdlet is the super set of all resources’ status.</span></span>
6.  <span data-ttu-id="56ca2-111">Состояние PendingReboot является супермножеством состояния PendingConfiguration.</span><span class="sxs-lookup"><span data-stu-id="56ca2-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

<span data-ttu-id="56ca2-112">В следующей таблице приведены итоговые свойства состояния в несколько типичных сценариях:</span><span class="sxs-lookup"><span data-stu-id="56ca2-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

| <span data-ttu-id="56ca2-113">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="56ca2-113">**Scenario**</span></span>                    | <span data-ttu-id="56ca2-114">**LCMState\***</span><span class="sxs-lookup"><span data-stu-id="56ca2-114">**LCMState\***</span></span>       | <span data-ttu-id="56ca2-115">**Состояние**</span><span class="sxs-lookup"><span data-stu-id="56ca2-115">**Status**</span></span> | <span data-ttu-id="56ca2-116">**Запрошена перезагрузка**</span><span class="sxs-lookup"><span data-stu-id="56ca2-116">**Reboot Requested**</span></span>  | <span data-ttu-id="56ca2-117">**ResourcesInDesiredState**</span><span class="sxs-lookup"><span data-stu-id="56ca2-117">**ResourcesInDesiredState**</span></span>  | <span data-ttu-id="56ca2-118">**ResourcesNotInDesiredState**</span><span class="sxs-lookup"><span data-stu-id="56ca2-118">**ResourcesNotInDesiredState**</span></span> |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| <span data-ttu-id="56ca2-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="56ca2-119">S**^**</span></span>                          | <span data-ttu-id="56ca2-120">Idle</span><span class="sxs-lookup"><span data-stu-id="56ca2-120">Idle</span></span>                 | <span data-ttu-id="56ca2-121">Успех</span><span class="sxs-lookup"><span data-stu-id="56ca2-121">Success</span></span>    | <span data-ttu-id="56ca2-122">$false</span><span class="sxs-lookup"><span data-stu-id="56ca2-122">$false</span></span>        | <span data-ttu-id="56ca2-123">S</span><span class="sxs-lookup"><span data-stu-id="56ca2-123">S</span></span>                            | <span data-ttu-id="56ca2-124">$null</span><span class="sxs-lookup"><span data-stu-id="56ca2-124">$null</span></span>                          |
| <span data-ttu-id="56ca2-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="56ca2-125">F**^**</span></span>                          | <span data-ttu-id="56ca2-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="56ca2-126">PendingConfiguration</span></span> | <span data-ttu-id="56ca2-127">Отказ</span><span class="sxs-lookup"><span data-stu-id="56ca2-127">Failure</span></span>    | <span data-ttu-id="56ca2-128">$false</span><span class="sxs-lookup"><span data-stu-id="56ca2-128">$false</span></span>        | <span data-ttu-id="56ca2-129">$null</span><span class="sxs-lookup"><span data-stu-id="56ca2-129">$null</span></span>                        | <span data-ttu-id="56ca2-130">F</span><span class="sxs-lookup"><span data-stu-id="56ca2-130">F</span></span>                              |
| <span data-ttu-id="56ca2-131">S,F</span><span class="sxs-lookup"><span data-stu-id="56ca2-131">S,F</span></span>                             | <span data-ttu-id="56ca2-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="56ca2-132">PendingConfiguration</span></span> | <span data-ttu-id="56ca2-133">Отказ</span><span class="sxs-lookup"><span data-stu-id="56ca2-133">Failure</span></span>    | <span data-ttu-id="56ca2-134">$false</span><span class="sxs-lookup"><span data-stu-id="56ca2-134">$false</span></span>        | <span data-ttu-id="56ca2-135">S</span><span class="sxs-lookup"><span data-stu-id="56ca2-135">S</span></span>                            | <span data-ttu-id="56ca2-136">F</span><span class="sxs-lookup"><span data-stu-id="56ca2-136">F</span></span>                              |
| <span data-ttu-id="56ca2-137">F,S</span><span class="sxs-lookup"><span data-stu-id="56ca2-137">F,S</span></span>                             | <span data-ttu-id="56ca2-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="56ca2-138">PendingConfiguration</span></span> | <span data-ttu-id="56ca2-139">Отказ</span><span class="sxs-lookup"><span data-stu-id="56ca2-139">Failure</span></span>    | <span data-ttu-id="56ca2-140">$false</span><span class="sxs-lookup"><span data-stu-id="56ca2-140">$false</span></span>        | <span data-ttu-id="56ca2-141">S</span><span class="sxs-lookup"><span data-stu-id="56ca2-141">S</span></span>                            | <span data-ttu-id="56ca2-142">F</span><span class="sxs-lookup"><span data-stu-id="56ca2-142">F</span></span>                              |
| <span data-ttu-id="56ca2-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="56ca2-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="56ca2-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="56ca2-144">PendingConfiguration</span></span> | <span data-ttu-id="56ca2-145">Отказ</span><span class="sxs-lookup"><span data-stu-id="56ca2-145">Failure</span></span>    | <span data-ttu-id="56ca2-146">$false</span><span class="sxs-lookup"><span data-stu-id="56ca2-146">$false</span></span>        | <span data-ttu-id="56ca2-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="56ca2-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="56ca2-148">F</span><span class="sxs-lookup"><span data-stu-id="56ca2-148">F</span></span>                              |
| <span data-ttu-id="56ca2-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="56ca2-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="56ca2-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="56ca2-150">PendingConfiguration</span></span> | <span data-ttu-id="56ca2-151">Отказ</span><span class="sxs-lookup"><span data-stu-id="56ca2-151">Failure</span></span>    | <span data-ttu-id="56ca2-152">$false</span><span class="sxs-lookup"><span data-stu-id="56ca2-152">$false</span></span>        | <span data-ttu-id="56ca2-153">S</span><span class="sxs-lookup"><span data-stu-id="56ca2-153">S</span></span>                            | <span data-ttu-id="56ca2-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="56ca2-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
| <span data-ttu-id="56ca2-155">S, r</span><span class="sxs-lookup"><span data-stu-id="56ca2-155">S, r</span></span>                            | <span data-ttu-id="56ca2-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="56ca2-156">PendingReboot</span></span>        | <span data-ttu-id="56ca2-157">Успех</span><span class="sxs-lookup"><span data-stu-id="56ca2-157">Success</span></span>    | <span data-ttu-id="56ca2-158">$true</span><span class="sxs-lookup"><span data-stu-id="56ca2-158">$true</span></span>         | <span data-ttu-id="56ca2-159">S</span><span class="sxs-lookup"><span data-stu-id="56ca2-159">S</span></span>                            | <span data-ttu-id="56ca2-160">r</span><span class="sxs-lookup"><span data-stu-id="56ca2-160">r</span></span>                              |
| <span data-ttu-id="56ca2-161">F, r</span><span class="sxs-lookup"><span data-stu-id="56ca2-161">F, r</span></span>                            | <span data-ttu-id="56ca2-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="56ca2-162">PendingReboot</span></span>        | <span data-ttu-id="56ca2-163">Отказ</span><span class="sxs-lookup"><span data-stu-id="56ca2-163">Failure</span></span>    | <span data-ttu-id="56ca2-164">$true</span><span class="sxs-lookup"><span data-stu-id="56ca2-164">$true</span></span>         | <span data-ttu-id="56ca2-165">$null</span><span class="sxs-lookup"><span data-stu-id="56ca2-165">$null</span></span>                        | <span data-ttu-id="56ca2-166">F, r</span><span class="sxs-lookup"><span data-stu-id="56ca2-166">F, r</span></span>                           |
| <span data-ttu-id="56ca2-167">r, S</span><span class="sxs-lookup"><span data-stu-id="56ca2-167">r, S</span></span>                            | <span data-ttu-id="56ca2-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="56ca2-168">PendingReboot</span></span>        | <span data-ttu-id="56ca2-169">Успех</span><span class="sxs-lookup"><span data-stu-id="56ca2-169">Success</span></span>    | <span data-ttu-id="56ca2-170">$true</span><span class="sxs-lookup"><span data-stu-id="56ca2-170">$true</span></span>         | <span data-ttu-id="56ca2-171">$null</span><span class="sxs-lookup"><span data-stu-id="56ca2-171">$null</span></span>                        | <span data-ttu-id="56ca2-172">r</span><span class="sxs-lookup"><span data-stu-id="56ca2-172">r</span></span>                              |
| <span data-ttu-id="56ca2-173">r, F</span><span class="sxs-lookup"><span data-stu-id="56ca2-173">r, F</span></span>                            | <span data-ttu-id="56ca2-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="56ca2-174">PendingReboot</span></span>        | <span data-ttu-id="56ca2-175">Успех</span><span class="sxs-lookup"><span data-stu-id="56ca2-175">Success</span></span>    | <span data-ttu-id="56ca2-176">$true</span><span class="sxs-lookup"><span data-stu-id="56ca2-176">$true</span></span>         | <span data-ttu-id="56ca2-177">$null</span><span class="sxs-lookup"><span data-stu-id="56ca2-177">$null</span></span>                        | <span data-ttu-id="56ca2-178">r</span><span class="sxs-lookup"><span data-stu-id="56ca2-178">r</span></span>                              |

<span data-ttu-id="56ca2-179">^ S<sub>i</sub>: ряд ресурсов, которые успешно применены F<sub>i</sub>: ряд ресурсов, которые применены неудачно r: ресурс, который требует перезагрузки.\*</span><span class="sxs-lookup"><span data-stu-id="56ca2-179">^ S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```
## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="56ca2-180">Улучшения в командлете Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="56ca2-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="56ca2-181">В этом выпуске в командлет Get-DscConfigurationStatus было внесено несколько улучшений.</span><span class="sxs-lookup"><span data-stu-id="56ca2-181">A few enhancements have been made to Get-DscConfigurationStatus cmdlet in this release.</span></span> <span data-ttu-id="56ca2-182">Ранее свойство StartDate объектов, возвращаемое командлетом StartDate, имело тип String.</span><span class="sxs-lookup"><span data-stu-id="56ca2-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="56ca2-183">Теперь оно имеет тип Datetime, что упрощает сложный выбор и фильтрацию благодаря встроенным свойствам объекта Datetime.</span><span class="sxs-lookup"><span data-stu-id="56ca2-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>
```powershell
(Get-DscConfigurationStatus).StartDate | fl \*
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

<span data-ttu-id="56ca2-184">Ниже приведен пример, который возвращает все записи операций DSC, созданные в тот же день недели, что и сегодня.</span><span class="sxs-lookup"><span data-stu-id="56ca2-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>
```powershell
(Get-DscConfigurationStatus –All) | where { $\_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="56ca2-185">Записи операций, которые не вносят изменения в конфигурацию узла (т. е. представлены операциями только для чтения), исключаются.</span><span class="sxs-lookup"><span data-stu-id="56ca2-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="56ca2-186">Таким образом, операции Test-DscConfiguration и Get-DscConfiguration больше не имитируются в возвращаемых объектах из командлета Get-DscConfigurationStatus.</span><span class="sxs-lookup"><span data-stu-id="56ca2-186">Therefore, Test-DscConfiguration, Get-DscConfiguration operations are no longer adulterated in returned objects from Get-DscConfigurationStatus cmdlet.</span></span>
<span data-ttu-id="56ca2-187">В выходные данные командлета Get-DscConfigurationStatus добавляются записи для операции настройки метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="56ca2-187">Records of meta configuration setting operation is added to the return of Get-DscConfigurationStatus cmdlet.</span></span>

<span data-ttu-id="56ca2-188">Ниже приведен пример результата, возвращаемого из командлета DscConfigurationStatus –All.</span><span class="sxs-lookup"><span data-stu-id="56ca2-188">Following is an example of result returned from Get-DscConfigurationStatus –All cmdlet.</span></span>
```powershell
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="56ca2-189">Улучшения в командлете Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="56ca2-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>
<span data-ttu-id="56ca2-190">В объект, возвращаемый из командлета Get-DscLocalConfigurationManager, добавлено новое поле LCMStateDetail.</span><span class="sxs-lookup"><span data-stu-id="56ca2-190">A new field of LCMStateDetail is added to the object returned from Get-DscLocalConfigurationManager cmdlet.</span></span> <span data-ttu-id="56ca2-191">Оно заполняется в том случае, когда LCMState имеет значение Busy.</span><span class="sxs-lookup"><span data-stu-id="56ca2-191">This field is populated when LCMState is “Busy”.</span></span> <span data-ttu-id="56ca2-192">Извлечь его можно с помощью следующего командлета:</span><span class="sxs-lookup"><span data-stu-id="56ca2-192">It can be retrieved by following cmdlet:</span></span>
```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="56ca2-193">Ниже приведен пример выходных данных для постоянного мониторинга конфигурации, которая требует двух перезагрузок на удаленном узле.</span><span class="sxs-lookup"><span data-stu-id="56ca2-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>
```powershell
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```
