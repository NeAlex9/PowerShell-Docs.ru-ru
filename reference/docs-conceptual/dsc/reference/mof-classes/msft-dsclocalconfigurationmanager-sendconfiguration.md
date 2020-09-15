---
ms.date: 07/17/2020
keywords: dsc,powershell,конфигурация,установка
title: Метод SendConfiguration
ms.openlocfilehash: afd6e8d7acc969df16fad1d0ba15c9fe0b1a26fd
ms.sourcegitcommit: 41e1acbd9ce0f49a23c6eb99facd2c280d836836
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2020
ms.locfileid: "86463947"
---
# <a name="sendconfiguration-method"></a><span data-ttu-id="8e077-103">Метод SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="8e077-103">SendConfiguration method</span></span>

<span data-ttu-id="8e077-104">Отправляет документ конфигурации на управляемый узел и сохраняет его как ожидающее изменение.</span><span class="sxs-lookup"><span data-stu-id="8e077-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

## <a name="syntax"></a><span data-ttu-id="8e077-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="8e077-105">Syntax</span></span>

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="8e077-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="8e077-106">Parameters</span></span>

<span data-ttu-id="8e077-107">**ConfigurationData** \[in\] Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e077-107">**ConfigurationData** \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="8e077-108">**force** \[in\] **true** Принудительная остановка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e077-108">**force** \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="8e077-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="8e077-109">Return value</span></span>

<span data-ttu-id="8e077-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="8e077-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="8e077-111">Remarks</span><span class="sxs-lookup"><span data-stu-id="8e077-111">Remarks</span></span>

<span data-ttu-id="8e077-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="8e077-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="8e077-113">Требования</span><span class="sxs-lookup"><span data-stu-id="8e077-113">Requirements</span></span>

<span data-ttu-id="8e077-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="8e077-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="8e077-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8e077-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="8e077-116">См. также раздел</span><span class="sxs-lookup"><span data-stu-id="8e077-116">See also</span></span>

[<span data-ttu-id="8e077-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="8e077-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
