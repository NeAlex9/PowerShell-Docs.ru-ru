---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
ms.openlocfilehash: 61c5df1b64cb9c54f9c7372a56e77abf319658dd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085145"
---
# <a name="network-switch-management-with-powershell"></a>Управление сетевыми коммутаторами с помощью PowerShell

Теперь командлет **Get-NetworkSwitchEthernetPort** возвращает вместе с экземплярами следующие дополнительные сведения.

- IPAddress — сопоставленный с портом IP-адрес
- PortMode — режим порта: доступ, маршрут или магистраль
- AccessVLAN — идентификатор виртуальной локальной сети, связанной с этим портом в режиме доступа
- TrunkedVLANList — список идентификаторов виртуальных локальных сетей, связанных с этим портом в режиме магистрали

## <a name="fundamental-network-switch-management-with-windows-powershell"></a>Основы управления сетевыми коммутаторами с помощью Windows PowerShell

Командлеты сетевых коммутаторов, представленные в WMF 5.0, позволяют применять конфигурацию коммутатора, виртуальной локальной сети и портов базового сетевого коммутатора уровня 2 к сетевым коммутаторам, прошедшим сертификацию для Windows Server 2012 R2. Корпорация Майкрософт по-прежнему придерживается концепции уровня [абстракции центра обработки данных](http://technet.microsoft.com/cloud/dal.aspx) (DAL) и стремится продемонстрировать ту пользу, которую она может принести нашим клиентам и партнерам. Эти командлеты позволяют осуществлять следующее.

- Глобальная конфигурация коммутаторов, например следующее.
    - Задание имени узла
    - Задание баннера параметров
    - Сохранение конфигурации
    - Включение и отключение функции

- Конфигурация виртуальной локальной сети:
    - Создание или удаление виртуальной ЛС
    - Включение или отключение виртуальной ЛС
    - Перечисление виртуальной ЛС
    - Указание понятного имени для виртуальной ЛС

- Конфигурация портов уровня 2:
    - Перечисление портов
    - Включение или отключение портов
    - Задание свойств и режимов портов
    - Добавление или сопоставление виртуальной ЛС с режимом магистрали или доступа для порта

Ознакомьтесь со всеми командлетами NetworkSwitch.

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

Дополнительные сведения см. в записи блога Джеффри Сновера (Jeffrey Snover), посвященной выпуску WMF 5.0 Preview: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx>
