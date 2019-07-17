---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Класс MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 09b30edd48384c0e8412e0e6ee926a719249c5b8
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726888"
---
# <a name="msftdsclocalconfigurationmanager-class"></a>Класс MSFT_DSCLocalConfigurationManager

Локальный диспетчер конфигураций (LCM) управляет состоянием файлов конфигурации и использует агент конфигурации для применения настроек.

Следующий пример синтаксиса — упрощенный MOF-код, который включает все наследуемые свойства.

## <a name="syntax"></a>Синтаксис

```
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a>Члены группы

Класс **MSFT_DSCLocalConfigurationManager** включает следующие члены:

- [Методы][]

### <a name="methods"></a>Методы

Класс **MSFT_DSCLocalConfigurationManager** включает следующие методы:

|Метод |Описание |
|:--- |:---|
| [ApplyConfiguration](msft-dsclocalconfigurationmanager-applyconfiguration.md)| Использует агент конфигурации для применения конфигурации, которая находится в состоянии ожидания.|
| [DisableDebugConfiguration](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| Отключает отладку ресурсов DSC.|
| [EnableDebugConfiguration](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| Включает отладку ресурсов DSC.|
| [GetConfiguration](msft-dsclocalconfigurationmanager-getconfiguration.md)| Отправляет документ конфигурации на управляемый узел и использует метод **Get** агента конфигурации для применения конфигурации.|
| [GetConfigurationResultOutput](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| Получает выходные данные агента конфигурации, относящиеся к определенному заданию.|
| [GetConfigurationStatus](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| Получает журнал состояния конфигурации.|
| [GetMetaConfiguration](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| Получает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.|
| [PerformRequiredConfigurationChecks](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| Запускает проверку согласованности.|
| [RemoveConfiguration](msft-dsclocalconfigurationmanager-removeconfiguration.md)| Удаляет файлы конфигурации.|
| [ResourceGet](msft-dsclocalconfigurationmanager-resourceget.md)| Напрямую вызывает метод **Get** ресурса DSC.|
| [ResourceSet](msft-dsclocalconfigurationmanager-resourceset.md)| Напрямую вызывает метод **Set** ресурса DSC.|
| [ResourceTest](msft-dsclocalconfigurationmanager-resourcetest.md)| Напрямую вызывает метод **Test** ресурса DSC.|
| [RollBack](msft-dsclocalconfigurationmanager-rollback.md)| Выполняет откат к предыдущей конфигурации.|
| [SendConfiguration](msft-dsclocalconfigurationmanager-sendconfiguration.md)| Отправляет документ конфигурации на управляемый узел и сохраняет его как ожидающее изменение.|
| [SendConfigurationApply](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| Отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.|
| [SendConfigurationApplyAsync](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| Отправляет документ конфигурации на управляемый узел и запускает агент конфигурации для применения конфигурации. Для получения выходных данных используется метод GetConfigurationResultOutput.|
| [SendMetaConfigurationApply](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| Задает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.|
| [StopConfiguration](msft-dsclocalconfigurationmanager-stopconfiguration.md)| Останавливает выполняемую конфигурацию.|
| [TestConfiguration](msft-dsclocalconfigurationmanager-testconfiguration.md)| Отправляет документ конфигурации на управляемый узел и проверяет соответствие текущей конфигурации документу.|

## <a name="requirements"></a>Требования

**MOF-файл:** DscCore.mof

**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration
