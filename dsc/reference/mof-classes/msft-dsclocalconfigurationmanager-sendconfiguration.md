---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 3529bc56ecba19ed0fbbf070a4e86d0692824d39
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55679711"
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5e618-103">Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="5e618-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5e618-104">Отправляет документ конфигурации на управляемый узел и сохраняет его как ожидающее изменение.</span><span class="sxs-lookup"><span data-stu-id="5e618-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

## <a name="syntax"></a><span data-ttu-id="5e618-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5e618-105">Syntax</span></span>

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="5e618-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="5e618-106">Parameters</span></span>

<span data-ttu-id="5e618-107">*ConfigurationData* \[in\] Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5e618-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="5e618-108">*force* \[in\] **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5e618-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="5e618-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5e618-109">Return value</span></span>

<span data-ttu-id="5e618-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="5e618-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5e618-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="5e618-111">Remarks</span></span>

<span data-ttu-id="5e618-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="5e618-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5e618-113">Требования</span><span class="sxs-lookup"><span data-stu-id="5e618-113">Requirements</span></span>

<span data-ttu-id="5e618-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5e618-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="5e618-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5e618-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="5e618-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="5e618-116">See also</span></span>

[<span data-ttu-id="5e618-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5e618-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)