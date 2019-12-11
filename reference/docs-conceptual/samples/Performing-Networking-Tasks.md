---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Выполнение задач по работе с сетями
ms.openlocfilehash: e581296b4b7609b374f206c447c4f797e3e2c400
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030861"
---
# <a name="performing-networking-tasks"></a>Выполнение задач по работе с сетями

Большая часть задач администрирования низкоуровневых сетевых протоколов связана с протоколом TCP/IP, так как это наиболее распространенный сетевой протокол. В этом разделе описано использование Windows PowerShell и WMI для выполнения этих задач.

## <a name="listing-ip-addresses-for-a-computer"></a>Получение списка IP-адресов компьютера

Список всех IP-адресов, используемых локальным компьютером, возвращает следующая команда:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

Выходные данные этой команды отличаются от большинства списков свойств заключением значений в фигурные скобки:

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

Чтобы понять причину появления скобок, используйте командлет Get-Member для изучения свойства **IPAddress**.

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

Свойство IPAddress каждого сетевого адаптера в действительности представляет собой массив. Фигурные скобки в определении указывают на то, что свойство **IPAddress** содержит не значение типа **System.String**, а массив значений типа **System.String**.

## <a name="listing-ip-configuration-data"></a>Вывод данных IP-конфигурации

Для отображения подробных данных IP-конфигурации каждого сетевого адаптера воспользуйтесь следующей командой:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

По умолчанию отображается очень небольшая часть доступных сведений об объекте конфигурации сетевого адаптера. Для более глубокого изучения и устранения неполадок воспользуйтесь командлетом Select-Object или командлетом форматирования, например Format-List, чтобы задать отображаемые свойства.

Если свойства IPX или WINS не представляют интереса (что характерно для современной сети TCP/IP), можно использовать параметр ExcludeProperty командлета Select-Object, чтобы скрыть свойства с именами, начинающимися на WINS или IPX.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

Эта команда выводит подробные сведения о DHCP, DNS, маршрутизации и других менее значительных свойствах IP-конфигурации.

## <a name="pinging-computers"></a>Проверка связи с компьютерами

Простую проверку связи с компьютером можно выполнить с помощью **Win32_PingStatus**. Следующая команда производит проверку связи, но при этом выводит большой объем сведений:

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

Удобнее отображать сводные данные, содержащие свойства Address, ResponseTime и StatusCode, как это делает приведенная ниже команда. Параметр Autosize командлета Format-Table изменяет размер столбцов таблицы для их правильного отображения в Windows PowerShell.

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

Значение 0 свойства StatusCode указывает на успешно выполненную проверку связи.

Для проверки связи с несколькими компьютерами с помощью одной команды можно использовать массив. Так как адресов несколько, для проверки связи с каждым адресом по отдельности можно использовать **ForEach-Object**.

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Один и тот же формат команды можно использовать для проверки связи со всеми компьютерами подсети. Например, при проверке частной сети, использующей номер сети 192.168.1.0 и стандартную маску подсети класса C (255.255.255.0), допустимы только локальные адреса в диапазоне от 192.168.1.1 до 192.168.1.254 (0 всегда зарезервирован в качестве номера сети, а 255 используется в качестве широковещательного адреса подсети).

Чтобы представить массив чисел от 1 до 254 в Windows PowerShell, используйте оператор **1..254**. Таким образом, полную проверку связи с подсетью можно осуществить, сформировав этот массив и добавляя его элементы к частичному адресу в операторе проверки связи:

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Такой метод формирования диапазона адресов может быть использован в любых подобных случаях. Полный набор адресов можно сформировать следующим образом:

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

## <a name="retrieving-network-adapter-properties"></a>Извлечение свойств сетевого адаптера

Ранее в данном руководстве пользователя упоминалось о возможности извлечения общих свойств конфигурации с помощью **Win32_NetworkAdapterConfiguration**. Такие сведения о сетевом адаптере, как MAC-адреса и типы адаптеров, не относятся, строго говоря, к протоколу TCP/IP, но могут оказаться полезными для понимания того, что происходит в компьютере. Сводные данные можно получить с помощью следующей команды:

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

## <a name="assigning-the-dns-domain-for-a-network-adapter"></a>Назначение домена DNS сетевому адаптеру

Чтобы назначить домен DNS для автоматического разрешения имен, нужно использовать метод **Win32_NetworkAdapterConfiguration SetDNSDomain**. Так как назначение домена DNS для каждого сетевого адаптера производится независимо, чтобы назначить домен для каждого адаптера, необходимо воспользоваться оператором **ForEach-Object**.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

Здесь нужно использовать оператор фильтрации "IPEnabled=$true", так как даже в сети, использующей лишь протокол TCP/IP, некоторые сетевые адаптеры компьютера не являются настоящими адаптерами TCP/IP. Они представляют собой общие программные элементы, поддерживающие службы RAS, PPTP, QoS и т. п. для всех адаптеров, и не имеют собственного адреса.

Фильтрацию в команде можно осуществить с помощью командлета **Where-Object** вместо фильтра **Get-WmiObject**.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

## <a name="performing-dhcp-configuration-tasks"></a>Выполнение задач настройки DHCP

Изменение сведений DHCP, так же как и настройка DNS, включает работу с набором сетевых адаптеров. Существует несколько отдельных действий, выполняемых с помощью инструментария WMI. Мы рассмотрим несколько наиболее типичных.

### <a name="determining-dhcp-enabled-adapters"></a>Определение адаптеров, поддерживающих DHCP

Найти на компьютере адаптеры, поддерживающие DHCP, можно с помощью следующей команды:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

Чтобы исключить из поиска адаптеры, имеющие проблемы в IP-конфигурации, можно добавить требование поддержки протокола IP:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

### <a name="retrieving-dhcp-properties"></a>Извлечение свойств DHCP

Свойства адаптера, относящиеся к протоколу DHCP, обычно начинаются с DHCP, поэтому для отображения только этих свойств можно использовать параметр Property командлета Format-Table:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

### <a name="enabling-dhcp-on-each-adapter"></a>Включение поддержки DHCP на каждом адаптере

Чтобы включить поддержку DHCP на всех адаптерах, используйте команду:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

Можно воспользоваться оператором **Filter** "IPEnabled=$true and DHCPEnabled=$false" во избежание включения поддержки DHCP для адаптеров, у которых она уже включена, но пропуск этого шага не приведет к появлению ошибок.

### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>Отмена и обновление аренды адреса DHCP для отдельных адаптеров

Класс **Win32_NetworkAdapterConfiguration** использует методы **ReleaseDHCPLease** и **RenewDHCPLease**. Оба метода используются одинаково. Обычно их применяют лишь при необходимости отмены или обновления аренды адресов для адаптера в отдельной подсети. Простейшим способом фильтрации адаптеров в подсети является выбор лишь тех адаптеров, которые используют шлюз для этой подсети. Например, следующая команда отменяет все аренды адресов DHCP для адаптеров на локальном компьютере, которые арендуют адреса DHCP с 192.168.1.254:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

Единственное отличие при обновлении аренды адреса DHCP состоит в вызове метода **RenewDHCPLease** вместо метода **ReleaseDHCPLease**:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Если эти методы применяются на удаленном компьютере, возможна потеря доступа к удаленной системе, которая подключена через адаптер с отмененной или обновленной арендой.

### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>Отмена и обновление аренды адресов DHCP для всех адаптеров

Отменить или обновить аренду адресов DHCP сразу для всех адаптеров можно с помощью методов **Win32_NetworkAdapterConfiguration** — **ReleaseDHCPLeaseAll** и **RenewDHCPLeaseAll**. Однако эту команду следует применять к классу WMI, а не к отдельному адаптеру, поскольку глобальная отмена и обновление аренды осуществляется на уровне класса, а не отдельного адаптера.

Ссылку на класс WMI вместо ссылки на экземпляры класса можно получить путем перечисления всех классов WMI и выбора нужного класса по имени. Например, следующая команда возвращает класс Win32_NetworkAdapterConfiguration:

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

Эту команду можно рассматривать как класс и использовать ее при вызове метода **ReleaseDHCPAdapterLease**. В следующей команде элементы конвейера **Get-WmiObject** и **Where-Object** ограничены круглыми скобками, поэтому Windows PowerShell обрабатывает их первыми:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

Такой же формат команды используется при вызове метода **RenewDHCPLeaseAll**:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

## <a name="creating-a-network-share"></a>Создание сетевой папки

Создать сетевую папку можно с помощью метода **Win32_Share Create**:

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

Для этой же цели в Windows PowerShell можно использовать команду **net share**:

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

## <a name="removing-a-network-share"></a>Удаление сетевой папки

Сетевую папку можно удалить с помощью **Win32_Share**, но этот процесс немного отличается от создания, так как требует получения именно удаляемой сетевой папки, а не класса **Win32_Share**. Следующий оператор удаляет сетевую папку TempShare:

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

В этом случае подойдет и **Net share**:

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

## <a name="connecting-a-windows-accessible-network-drive"></a>Подключение сетевого диска, доступного в Windows

Командлет **New-PSDrive** позволяет создавать диски Windows PowerShell, но они доступны только в Windows PowerShell. Для создания сетевого диска можно воспользоваться COM-объектом **WScript.Network**. Следующая команда сопоставляет сетевую папку \\\\FPS01\\users с локальным диском B:

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

Так же работает и команда **net use**:

```powershell
net use B: \\FPS01\users
```

Диски, сопоставленные с помощью **WScript.Network** или команды net use, мгновенно становятся доступными в Windows PowerShell.
