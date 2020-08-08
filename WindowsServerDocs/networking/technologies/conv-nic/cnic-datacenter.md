---
title: Конвергенция сетевого адаптера в групповой конфигурации сетевого адаптера (центр обработки данных)
description: В этом разделе мы предоставляющи инструкции по развертыванию Объединенной сетевой карты в групповой конфигурации сетевого адаптера с включенным объединением коммутаторов (SET).
ms.topic: article
ms.assetid: f01546f8-c495-4055-8492-8806eee99862
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/17/2018
ms.openlocfilehash: 918b3d10c39c6f06330f9c0986bc08b5bc04a229
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949378"
---
# <a name="converged-nic-in-a-teamed-nic-configuration-datacenter"></a>Конвергенция сетевого адаптера в групповой конфигурации сетевого адаптера (центр обработки данных)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе приведены инструкции по развертыванию Объединенной сетевой карты в групповой конфигурации сетевого адаптера с набором команд коммутатора Embedded \( \) .

В примере конфигурации в этом разделе описываются два узла Hyper-v, **узел 1** и **узел Hyper**-v 2. Оба узла имеют два сетевых адаптера. На каждом узле один адаптер подключен к подсети 192.168.1. x/24, а один адаптер подключен к подсети 192.168.2. x/24.

![Узлы Hyper-V](../../media/Converged-NIC/1-datacenter-test-conn.jpg)

## <a name="step-1-test-the-connectivity-between-source-and-destination"></a>Шаг 1. Проверка подключения между источником и назначением

Убедитесь, что физический сетевой адаптер может подключаться к целевому узлу.  В этом тесте демонстрируется подключение с помощью третьего уровня 3 \( \) или уровня IP, а также виртуальной \( локальной сети уровня 2 L2 \) \( \) .

1. Просмотр свойств первого сетевого адаптера.

   ```powershell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**Результаты**_


   |    name    |           интерфацедескриптион           | ifIndex | Состояние |    MacAddress     | LinkSpeed |
   |------------|------------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-1 | Ethernet-адаптер Mellanox ConnectX-3 Pro |   11    |   Up   | E4-1D-2D-07-43-D0 |  40 Гбит/с  |

2. Просмотр дополнительных свойств для первого адаптера, включая IP-адрес.

   ```powershell
   Get-NetIPAddress -InterfaceAlias "Test-40G-1"
   Get-NetIPAddress -InterfaceAlias "TEST-40G-1" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**Результаты**_


   |   Параметр    |    Значение    |
   |----------------|-------------|
   |   IPAddress    | 192.168.1.3 |
   | InterfaceIndex |     11      |
   | InterfaceAlias | Test-40G-1  |
   | AddressFamily  |    IPv4     |
   |      Тип      |   Одноадресная рассылка   |
   |  PrefixLength  |     24      |

3. Просмотрите свойства второго сетевого адаптера.

   ```powershell
   Get-NetAdapter -Name "Test-40G-2" | ft -AutoSize
   ```

   _**Результаты**_


   |    name    |          интерфацедескриптион           | ifIndex | Состояние |    MacAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | TEST-40G-2 | Mellanox ConnectX-3 Pro Ethernet A... #2 |   13    |   Up   | E4-1D-2D-07-40-70 |  40 Гбит/с  |

4. Просмотрите дополнительные свойства для второго адаптера, включая IP-адрес.

   ```powershell
   Get-NetIPAddress -InterfaceAlias "Test-40G-2"
   Get-NetIPAddress -InterfaceAlias "Test-40G-2" | Where-Object {$_.AddressFamily -eq "IPv4"} | fl InterfaceAlias,IPAddress
   ```

   _**Результаты**_


   |   Параметр    |    Значение    |
   |----------------|-------------|
   |   IPAddress    | 192.168.2.3 |
   | InterfaceIndex |     13      |
   | InterfaceAlias | TEST-40G-2  |
   | AddressFamily  |    IPv4     |
   |      Тип      |   Одноадресная рассылка   |
   |  PrefixLength  |     24      |

5. Убедитесь, что у других команд сетевой карты или набора Пникс есть допустимый IP-адрес.<p>Используйте отдельную подсеть \( xxx.xxx.** 2**. XXX vs XXX.xxx. **1**. XXX \) , чтобы упростить отправку из этого адаптера в место назначения. В противном случае, если вы обнаружите обе Пникс в одной подсети, балансировка нагрузки стека TCP/IP в Windows для интерфейсов и простая проверка станет более сложной.


## <a name="step-2-ensure-that-source-and-destination-can-communicate"></a>Шаг 2. Убедитесь, что источник и назначение могут обмениваться данными

На этом шаге мы используем команду Windows PowerShell **Test-NetConnection** , но если хотите, можно использовать команду **ping** .

1. Проверьте двунаправленный обмен данными.

   ```powershell
   Test-NetConnection 192.168.1.5
   ```

   _**Результаты**_


   |        Параметр         |    Значение    |
   |--------------------------|-------------|
   |       ИмяКомпьютера       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | Test-40G-1  |
   |      саурцеаддресс       | 192.168.1.3 |
   |      пингсукцеедед       |    Неверно    |
   | \(RTT пингреплидетаилс\) |    0 мс     |

   В некоторых случаях для успешного выполнения этого теста может потребоваться отключить брандмауэр Windows в расширенной безопасности. При отключении брандмауэра учитывайте безопасность и убедитесь, что ваша конфигурация соответствует требованиям безопасности вашей организации.

2. Отключите все профили брандмауэра.

   ```powershell
   Set-NetFirewallProfile -All -Enabled False
   ```

3. После отключения профилей брандмауэра снова проверьте подключение.

   ```powershell
   Test-NetConnection 192.168.1.5
   ```

   _**Результаты**_


   |        Параметр         |    Значение    |
   |--------------------------|-------------|
   |       ИмяКомпьютера       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | Test-40G-1  |
   |      саурцеаддресс       | 192.168.1.3 |
   |      пингсукцеедед       |    Неверно    |
   | \(RTT пингреплидетаилс\) |    0 мс     |


4. Проверьте подключение к дополнительным сетевым картам. Повторите предыдущие шаги для всех последующих Пникс, входящих в сетевую карту или команду SET Team.

   ```powershell
   Test-NetConnection 192.168.2.5
   ```

   _**Результаты**_


   |        Параметр         |    Значение    |
   |--------------------------|-------------|
   |       ИмяКомпьютера       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | Test-40G-2  |
   |      саурцеаддресс       | 192.168.2.3 |
   |      пингсукцеедед       |    Неверно    |
   | \(RTT пингреплидетаилс\) |    0 мс     |

## <a name="step-3-configure-the-vlan-ids-for-nics-installed-in-your-hyper-v-hosts"></a>Шаг 3. Настройка идентификаторов виртуальных ЛС для сетевых адаптеров, установленных на узлах Hyper-V

Многие конфигурации сети используют виртуальные ЛС, и если вы планируете использовать виртуальные ЛС в сети, необходимо повторить предыдущий тест с настроенными виртуальными ЛС.

Для этого шага сетевые карты находятся в режиме **доступа** . Однако при создании виртуального коммутатора vSwitch Hyper-V \( \) позднее в этом пошаговом окне Свойства VLAN применяются на уровне порта vSwitch.

Так как коммутатор может содержать несколько виртуальных ЛС, для верхней части физического коммутатора Tor в стойке необходимо, чтобы \( \) порт, к которому подключен узел, был настроен в режиме магистрали.

>[!NOTE]
>Дополнительные сведения о настройке режима магистрали для коммутатора см. в документации по коммутатору ToR.

На следующем рисунке показаны два узла Hyper-V с двумя сетевыми адаптерами, которые имеют виртуальные ЛС 101 и VLAN 102, настроенные в свойствах сетевого адаптера.

![Настройка виртуальных локальных сетей](../../media/Converged-NIC/2-datacenter-configure-vlans.jpg)


>[!TIP]
>В соответствии с институтами стандартов сетей IEEE для электропитания и электроники \( \) , свойства качества обслуживания \( \) в физическом сетевом адаптере работают в заголовке 802.1 p, который внедряется в заголовок 802.1 q, \( \) при настройке идентификатора виртуальной ЛС.

1. Настройте идентификатор виртуальной ЛС на первом сетевом адаптере, Test-40G-1.

   ```powershell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "101"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-1" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**Результаты**_


   |    name    | DisplayName | DisplayValue | регистрикэйворд | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | TEST-40G-1 |   ИД виртуальной ЛС   |     101      |     VlanID      |     {101}     |

2. Перезапустите сетевой адаптер, чтобы применить идентификатор виртуальной ЛС.

   ```powershell
   Restart-NetAdapter -Name "Test-40G-1"
   ```

3. Убедитесь, что состояние **имеет значение работает.**

   ```powershell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**Результаты**_


   |    name    |          интерфацедескриптион           | ifIndex | Состояние |    MacAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-1 | Mellanox ConnectX-3 Pro Ethernet Ada... |   11    |   Up   | E4-1D-2D-07-43-D0 |  40 Гбит/с  |

4. Настройте идентификатор виртуальной ЛС во втором сетевом адаптере, Test-40G-2.

   ```powershell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "102"
   Get-NetAdapterAdvancedProperty -Name "Test-40G-2" | Where-Object {$_.RegistryKeyword -eq "VlanID"} | ft -AutoSize
   ```

   _**Результаты**_


   |    name    | DisplayName | DisplayValue | регистрикэйворд | RegistryValue |
   |------------|-------------|--------------|-----------------|---------------|
   | TEST-40G-2 |   ИД виртуальной ЛС   |     102      |     VlanID      |     {102}     |

5. Перезапустите сетевой адаптер, чтобы применить идентификатор виртуальной ЛС.

   ```powershell
   Restart-NetAdapter -Name "Test-40G-2"
   ```

6. Убедитесь, что состояние **имеет значение работает.**

   ```powershell
   Get-NetAdapter -Name "Test-40G-1" | ft -AutoSize
   ```

   _**Результаты**_


   |    name    |          интерфацедескриптион           | ifIndex | Состояние |    MacAddress     | LinkSpeed |
   |------------|-----------------------------------------|---------|--------|-------------------|-----------|
   | Test-40G-2 | Mellanox ConnectX-3 Pro Ethernet Ada... |   11    |   Up   | E4-1D-2D-07-43-D1 |  40 Гбит/с  |

   >[!IMPORTANT]
   >Перезапуск и доступность устройства в сети может занять несколько секунд.

7. Проверьте подключение для первой сетевой карты, Test-40G-1.<p>Если подключение не работает, проверьте конфигурацию виртуальной ЛС коммутатора или участие назначения в одной виртуальной ЛС.

   ```powershell
   Test-NetConnection 192.168.1.5
   ```

   _**Результаты**_


   |        Параметр         |    Значение    |
   |--------------------------|-------------|
   |       ИмяКомпьютера       | 192.168.1.5 |
   |      RemoteAddress       | 192.168.1.5 |
   |      InterfaceAlias      | Test-40G-1  |
   |      саурцеаддресс       | 192.168.1.5 |
   |      пингсукцеедед       |    True     |
   | \(RTT пингреплидетаилс\) |    0 мс     |

8. Проверьте подключение для первого сетевого адаптера, Test-40G-2.<p>Если подключение не работает, проверьте конфигурацию виртуальной ЛС коммутатора или участие назначения в одной виртуальной ЛС.

   ```powershell
   Test-NetConnection 192.168.2.5
   ```

   _**Результаты**_


   |        Параметр         |    Значение    |
   |--------------------------|-------------|
   |       ИмяКомпьютера       | 192.168.2.5 |
   |      RemoteAddress       | 192.168.2.5 |
   |      InterfaceAlias      | Test-40G-2  |
   |      саурцеаддресс       | 192.168.2.3 |
   |      пингсукцеедед       |    True     |
   | \(RTT пингреплидетаилс\) |    0 мс     |

   >[!IMPORTANT]
   >Нечастое выполнение **теста-NetConnection** или проверка связи не происходит сразу после выполнения **restart-NetAdapter**.  Подождите, пока завершится полная инициализация сетевого адаптера, и повторите попытку.
   >
   >Если подключения VLAN 101 работают, но подключения VLAN 102 нет, то проблема может быть в том, что коммутатор должен быть настроен так, чтобы разрешить трафик через порт для нужной виртуальной ЛС. Это можно проверить, временно установив неисправные адаптеры в VLAN 101 и повторив проверку подключения.


   На следующем рисунке показаны узлы Hyper-V после успешной настройки виртуальных ЛС.

   ![Настройка качества обслуживания](../../media/Converged-NIC/3-datacenter-configure-qos.jpg)


## <a name="step-4-configure-quality-of-service-qos"></a>Шаг 4. Настройка качества обслуживания \( QoS\)

>[!NOTE]
>Необходимо выполнить все этапы настройки DCB и QoS на всех узлах, предназначенных для взаимодействия друг с другом.

1. Установите мосты центра обработки \( данных \) на каждом узле Hyper-V.

   - **Необязательно** для сетевых конфигураций, использующих iWarp.
   - **Требуется** для сетевых конфигураций, использующих роце \( любую версию \) служб RDMA.

   ```powershell
   Install-WindowsFeature Data-Center-Bridging
   ```

   _**Результаты**_


   | Успешно | Требуется перезагрузка | Код завершения |     Результат функции     |
   |---------|----------------|-----------|------------------------|
   |  True   |       Нет       |  Успешно  | {Мост центра обработки данных} |

2. Задайте политики качества обслуживания для протокола SMB Direct:

   - **Необязательно** для сетевых конфигураций, использующих iWarp.
   - **Требуется** для сетевых конфигураций, использующих роце \( любую версию \) служб RDMA.

   В приведенной ниже команде примера значение «3» является произвольным. Можно использовать любое значение от 1 до 7, если одно и то же значение постоянно используется во всей конфигурации политик качества обслуживания.

   ```powershell
   New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
   ```

   _**Результаты**_


   |   Параметр    |          Значение           |
   |----------------|--------------------------|
   |      Имя      |           SMB            |
   |     Владелец      | Групповая политика \( машины\) |
   | NetworkProfile |           Все            |
   |   Приоритет   |           127            |
   |   жобобжект    |          &nbsp;          |
   | нетдиректпорт  |           445            |
   | приоритивалуе  |            3             |

3. Задайте дополнительные политики качества обслуживания для другого трафика в интерфейсе.

   ```powershell
   New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 0
   ```

   _**Результаты**_


   |   Параметр    |          Значение           |
   |----------------|--------------------------|
   |      Имя      |         DEFAULT          |
   |     Владелец      | Групповая политика \( машины\) |
   | NetworkProfile |           Все            |
   |   Приоритет   |           127            |
   |    Шаблон    |         Значение по умолчанию          |
   |   жобобжект    |          &nbsp;          |
   | приоритивалуе  |            0             |

4. Включите **Управление потоком приоритета** для трафика SMB, который не требуется для iWarp.

   ```powershell
   Enable-NetQosFlowControl -priority 3
   Get-NetQosFlowControl
   ```

   _**Результаты**_


   | Приоритет | Включено | Параметр Policy | IfIndex | ифалиас |
   |----------|---------|-----------|---------|---------|
   |    0     |  Неверно  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    1     |  False  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    2     |  Неверно  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    3     |  True   |  Глобальный   | &nbsp;  | &nbsp;  |
   |    4     |  Неверно  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    5     |  Неверно  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    6     |  Неверно  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    7     |  Неверно  |  Глобальный   | &nbsp;  | &nbsp;  |

   >**Важно!** Если результаты не соответствуют этим результатам, так как элементы, отличные от 3, имеют включенное значение true, необходимо отключить **фловконтрол** для этих классов.
   >
   >```powershell
   >Disable-NetQosFlowControl -priority 0,1,2,4,5,6,7
   >Get-NetQosFlowControl
   >```
   >В более сложных конфигурациях другим классам трафика может потребоваться управление потоком, однако эти сценарии выходят за рамки данного руководством.


5. Включите качество обслуживания для первой сетевой карты, Test-40G-1.

   ```powershell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-1"
   Get-NetAdapterQos -Name "Test-40G-1"

   Name: TEST-40G-1
   Enabled: True
   ```

   _**Возможности**:_


   |      Параметр      |   Оборудование   |   Текущий    |
   |---------------------|--------------|--------------|
   |    максекбипасс     | NotSupported | NotSupported |
   |     дкбкссуппорт     |     Отсутствуют     |     Отсутствуют     |
   | Нумткс (Max/ETS/коэффициент мощности) |    8/8/8     |    8/8/8     |

   _**Оператионалтраффикклассес**:_


   | TC |  TSA   | Пропускная способность | Приоритеты |
   |----|--------|-----------|------------|
   | 0  | Strict |  &nbsp;   |    0-7     |

   _**Оператионалфловконтрол**:_

   Приоритет 3 включен

   _**Оператионалклассификатионс**:_


   | Протокол  | Порт/тип | Приоритет |
   |-----------|-----------|----------|
   |  По умолчанию  |  &nbsp;   |    0     |
   | нетдирект |    445    |    3     |

6. Включите QoS для второй сетевой карты, Test-40G-2.

   ```powershell
   Enable-NetAdapterQos -InterfaceAlias "Test-40G-2"
   Get-NetAdapterQos -Name "Test-40G-2"

   Name: TEST-40G-2
   Enabled: True
   ```

   _**Возможности**:_


   |      Параметр      |   Оборудование   |   Текущий    |
   |---------------------|--------------|--------------|
   |    максекбипасс     | NotSupported | NotSupported |
   |     дкбкссуппорт     |     Отсутствуют     |     Отсутствуют     |
   | Нумткс (Max/ETS/коэффициент мощности) |    8/8/8     |    8/8/8     |

   _**Оператионалтраффикклассес**:_


   | TC |  TSA   | Пропускная способность | Приоритеты |
   |----|--------|-----------|------------|
   | 0  | Strict |  &nbsp;   |    0-7     |

    _**Оператионалфловконтрол**:_

    Приоритет 3 включен

   _**Оператионалклассификатионс**:_


   | Протокол  | Порт/тип | Приоритет |
   |-----------|-----------|----------|
   |  По умолчанию  |  &nbsp;   |    0     |
   | нетдирект |    445    |    3     |


7. Резервирование половины полосы пропускания в SMB Direct \( RDMA\)

   ```powershell
   New-NetQosTrafficClass "SMB" -priority 3 -bandwidthpercentage 50 -algorithm ETS
   ```

   _**Результаты**_


   | name | Алгоритм | Пропускная способность (%) | Приоритет | Параметр Policy | IfIndex | ифалиас |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | SMB  |    ETS    |      50      |    3     |  Глобальный   | &nbsp;  | &nbsp;  |

8. Просмотр параметров резервирования пропускной способности:

   ```powershell
   Get-NetQosTrafficClass | ft -AutoSize
   ```

   _**Результаты**_

   |   name    | Алгоритм | Пропускная способность (%) | Приоритет | Параметр Policy | IfIndex | ифалиас |
   |-----------|-----------|--------------|----------|-----------|---------|---------|
   | Параметры |    ETS    |      50      | 0 – 2, 4 – 7  |  Глобальный   | &nbsp;  | &nbsp;  |
   |    SMB    |    ETS    |      50      |    3     |  Глобальный   | &nbsp;  | &nbsp;  |

9. Используемых Создайте два дополнительных класса трафика для IP-трафика клиента.

   >[!TIP]
   >Можно опустить значения "IP1" и "IP2".

   ```powershell
   New-NetQosTrafficClass "IP1" -Priority 1 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**Результаты**_

   | name | Алгоритм | Пропускная способность (%) | Приоритет | Параметр Policy | IfIndex | ифалиас |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP1  |    ETS    |      10      |    1     |  Глобальный   | &nbsp;  | &nbsp;  |

   ```powershell
   New-NetQosTrafficClass "IP2" -Priority 2 -bandwidthpercentage 10 -algorithm ETS
   ```

   _**Результаты**_


   | name | Алгоритм | Пропускная способность (%) | Приоритет | Параметр Policy | IfIndex | ифалиас |
   |------|-----------|--------------|----------|-----------|---------|---------|
   | IP2  |    ETS    |      10      |    2     |  Глобальный   | &nbsp;  | &nbsp;  |

1.  Просмотр классов трафика QoS.

    ```powershell
    Get-NetQosTrafficClass | ft -AutoSize
    ```

    _**Результаты**_


    |   name    | Алгоритм | Пропускная способность (%) | Приоритет | Параметр Policy | IfIndex | ифалиас |
    |-----------|-----------|--------------|----------|-----------|---------|---------|
    | Параметры |    ETS    |      30      |  0, 4 — 7   |  Глобальный   | &nbsp;  | &nbsp;  |
    |    SMB    |    ETS    |      50      |    3     |  Глобальный   | &nbsp;  | &nbsp;  |
    |    IP1    |    ETS    |      10      |    1     |  Глобальный   | &nbsp;  | &nbsp;  |
    |    IP2    |    ETS    |      10      |    2     |  Глобальный   | &nbsp;  | &nbsp;  |

    ---

2.  Используемых Переопределите отладчик.<p>По умолчанию присоединенный отладчик блокирует NetQos.

    ```powershell
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 –Force
    Get-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" | ft AllowFlowControlUnderDebugger
    ```

    _**Результаты**_

    ```
    AllowFlowControlUnderDebugger
    -----------------------------
    1
    ```

## <a name="step-5-verify-the-rdma-configuration-mode-1"></a>Шаг 5. Проверка режима конфигурации RDMA \( 1\)

Перед созданием vSwitch и переходом в режим RDMA 2 необходимо убедиться, что структура настроена правильно \( \) .

На следующем рисунке показано текущее состояние узлов Hyper-V.

![Тест RDMA](../../media/Converged-NIC/4-datacenter-test-rdma.jpg)


1. Проверьте конфигурацию RDMA.

   ```powershell
   Get-NetAdapterRdma | ft -AutoSize
   ```

   _**Результаты**_


   |    name    |        интерфацедескриптион        | Включено |
   |------------|------------------------------------|---------|
   | TEST-40G-1 | Адаптер Mellanox ConnectX-4 VPI #2 |  True   |
   | TEST-40G-2 |  Адаптер Mellanox ConnectX-4 VPI   |  True   |

2. Определите значение **ifIndex** для целевых адаптеров.<p>Это значение используется в последующих шагах при запуске скачанного скрипта.

   ```powershell
   Get-NetIPConfiguration -InterfaceAlias "TEST*" | ft InterfaceAlias,InterfaceIndex,IPv4Address
   ```

   _**Результаты**_


   | InterfaceAlias | InterfaceIndex |  IPv4-адрес  |
   |----------------|----------------|---------------|
   |   TEST-40G-1   |       14       | {192.168.1.3} |
   |   TEST-40G-2   |       13       | {192.168.2.3} |

3. Скачайте [служебную программуDiskSpd.exe](https://aka.ms/diskspd) и извлеките ее в C:\TEST.\.

4. Скачайте [сценарий PowerShell Test-RDMA](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1) в тестовую папку на локальном диске, например C:\TEST\.

5. Запустите сценарий PowerShell **Test-Rdma.ps1** , чтобы передать значение ifIndex в сценарий, а также IP-адрес первого удаленного адаптера в той же виртуальной ЛС.<p>В этом примере сценарий передает значение **ifIndex** , равное 14, на IP-адрес удаленного сетевого адаптера 192.168.1.5.

   ```powershell
   C:\TEST\Test-RDMA.PS1 -IfIndex 14 -IsRoCE $true -RemoteIpAddress 192.168.1.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Результаты**_

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter M2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.1.5, is reachable.
   VERBOSE: Remote IP 192.168.1.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 662979201 RDMA bytes written per second
   VERBOSE: 37561021 RDMA bytes sent per second
   VERBOSE: 1023098948 RDMA bytes written per second
   VERBOSE: 8901349 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.1.5
   ```

   >[!NOTE]
   >Если трафик RDMA завершается неудачно, в Роце случае проверьте конфигурацию коммутатора ToR на соответствие параметрам коэффициента мощности или ETS, которые должны соответствовать параметрам узла. Справочные сведения см. в разделе "качество обслуживания" этого документа.

6. Запустите сценарий PowerShell **Test-Rdma.ps1** , чтобы передать значение ifIndex в сценарий, а также IP-адрес второго удаленного адаптера в той же виртуальной ЛС.<p>В этом примере сценарий передает значение **ifIndex** , равное 13, на IP-адрес удаленного сетевого адаптера 192.168.2.5.

   ```powershell
   C:\TEST\Test-RDMA.PS1 -IfIndex 13 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Результаты**_

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter TEST-40G-2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
   VERBOSE: Remote IP 192.168.2.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 541185606 RDMA bytes written per second
   VERBOSE: 34821478 RDMA bytes sent per second
   VERBOSE: 954717307 RDMA bytes written per second
   VERBOSE: 35040816 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
   ```

## <a name="step-6-create-a-hyper-v-vswitch-on-your-hyper-v-hosts"></a>Шаг 6. Создание Hyper-V vSwitch на узлах Hyper-V


На следующем рисунке показан узел Hyper-V 1 с vSwitch.

![Создание виртуального коммутатора Hyper-V](../../media/Converged-NIC/5-datacenter-create-vswitch.jpg)

1. Создайте vSwitch в режиме SET на узле Hyper-V 1.

   ```powershell
   New-VMSwitch –Name "VMSTEST" –NetAdapterName "TEST-40G-1","TEST-40G-2" -EnableEmbeddedTeaming $true -AllowManagementOS $true
   ```

   _**Результат**_


   |  name   | свитчтипе | нетадаптеринтерфацедескриптион |
   |---------|------------|--------------------------------|
   | вмстест |  Внешняя  |        Групповой интерфейс        |

2. Просмотрите группу физических адаптеров в НАБОРе.

   ```powershell
   Get-VMSwitchTeam -Name "VMSTEST" | fl
   ```

   _**Результаты**_

   ```
   Name: VMSTEST
   Id: ad9bb542-dda2-4450-a00e-f96d44bdfbec
   NetAdapterInterfaceDescription: {Mellanox ConnectX-3 Pro Ethernet Adapter, Mellanox ConnectX-3 Pro Ethernet Adapter #2}
   TeamingMode: SwitchIndependent
   LoadBalancingAlgorithm: Dynamic
   ```

3. Отображение двух представлений узла vNIC

   ```powershell
    Get-NetAdapter
   ```

   _**Результаты**_


   |        name         |        интерфацедескриптион         | ifIndex | Состояние |    MacAddress     | LinkSpeed |
   |---------------------|-------------------------------------|---------|--------|-------------------|-----------|
   | Адаптера vethernet (ВМСТЕСТ) | #2 адаптера виртуальной сети Ethernet Hyper-V |   28    |   Up   | E4-1D-2D-07-40-71 |  80 Гбит/с  |

4. Просмотрите дополнительные свойства узла vNIC.

   ```powershell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Результаты**_


   |  name   | исманажементос | VMName  |  SwitchName  | MacAddress | Состояние | IPAddresses |
   |---------|----------------|---------|--------------|------------|--------|-------------|
   | вмстест |      True      | вмстест | E41D2D074071 |    '    | &nbsp; |             |


5. Проверьте сетевое подключение к удаленному адаптеру виртуальной ЛС 101.

   ```powershell
   Test-NetConnection 192.168.1.5
   ```

   _**Результаты**_

   ```
   WARNING: Ping to 192.168.1.5 failed -- Status: DestinationHostUnreachable

   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (CORP-External-Switch)
   SourceAddress  : 10.199.48.170
   PingSucceeded  : False
   PingReplyDetails (RTT) : 0 ms
   ```

## <a name="step-7-remove-the-access-vlan-setting"></a>Шаг 7. Удаление параметра Access VLAN

На этом шаге вы удалите параметр ACCESS VLAN из физического сетевого адаптера и установите VLANID с помощью vSwitch.

Необходимо удалить параметр доступа VLAN, чтобы предотвратить автоматическое добавление тегов в исходящий трафик с неверным ИДЕНТИФИКАТОРом виртуальной ЛС и фильтрацию входящего трафика, который не соответствует ИДЕНТИФИКАТОРу виртуальной ЛС доступа.

1. Удалите параметр.

   ```powershell
   Set-NetAdapterAdvancedProperty -Name "Test-40G-1" -RegistryKeyword VlanID -RegistryValue "0"
   Set-NetAdapterAdvancedProperty -Name "Test-40G-2" -RegistryKeyword VlanID -RegistryValue "0"
   ```

2. Задайте идентификатор виртуальной ЛС.

   ```powershell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "VMSTEST" -VlanId "101" -Access -ManagementOS
   Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName "VMSTEST"
   ```

   _**Результаты**_

   ```
   VMName VMNetworkAdapterName Mode   VlanList
   ------ -------------------- ----   --------
          VMSTEST              Access 101
   ```


3. Проверьте сетевое подключение.

   ```powershell
   Test-NetConnection 192.168.1.5
   ```

   _**Результаты**_

   ```
   ComputerName   : 192.168.1.5
   RemoteAddress  : 192.168.1.5
   InterfaceAlias : vEthernet (VMSTEST)
   SourceAddress  : 192.168.1.3
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

   >**Важно!** Если результаты не похожи на примеры результатов и проверка связи завершается с сообщением "предупреждение: Проверка связи с 192.168.1.5 сбоем--Status: Дестинатионхостунреачабле", убедитесь, что "адаптера vethernet (ВМСТЕСТ)" имеет правильный IP-адрес.
   >
   >```powershell
   >Get-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)"
   >```
   >
   >Если IP-адрес не задан, устраните ошибку.
   >
   >```powershell
   >New-NetIPAddress -InterfaceAlias "vEthernet (VMSTEST)" -IPAddress 192.168.1.3 -PrefixLength 24
   >
   >IPAddress : 192.168.1.3
   >InterfaceIndex: 37
   >InterfaceAlias: vEthernet (VMSTEST)
   >AddressFamily : IPv4
   >Type  : Unicast
   >PrefixLength  : 24
   >PrefixOrigin  : Manual
   >SuffixOrigin  : Manual
   >AddressState  : Tentative
   >ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   >PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   >SkipAsSource  : False
   >PolicyStore   : ActiveStore
   >```


4. Переименуйте сетевой адаптер управления.

   ```powershell
   Rename-VMNetworkAdapter -ManagementOS -Name “VMSTEST” -NewName “MGT”
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Результаты**_


   |         name         | исманажементос | VMName |      SwitchName      |  MacAddress  | Состояние | IPAddresses |
   |----------------------|----------------|--------|----------------------|--------------|--------|-------------|
   | CORP — внешний коммутатор |      True      | &nbsp; | CORP — внешний коммутатор | 001B785768AA |  '  |   &nbsp;    |
   |         СКЛАД          |      True      | &nbsp; |       вмстест        | E41D2D074071 |  '  |   &nbsp;    |

5. Просмотр дополнительных свойств сетевого адаптера.

   ```powershell
   Get-NetAdapter
   ```

   _**Результаты**_


   |      name       |        интерфацедескриптион         | ifIndex | Состояние |    MacAddress     | LinkSpeed |
   |-----------------|-------------------------------------|---------|--------|-------------------|-----------|
   | Адаптера vethernet (центр) | #2 адаптера виртуальной сети Ethernet Hyper-V |   28    |   Up   | E4-1D-2D-07-40-71 |  80 Гбит/с  |

## <a name="step-8-test-hyper-v-vswitch-rdma"></a>Шаг 8. Тестирование Hyper-V vSwitch RDMA

На следующем рисунке показано текущее состояние узлов Hyper-V, включая vSwitch на узле Hyper-V 1.

![Тестирование виртуального коммутатора Hyper-V](../../media/Converged-NIC/6-datacenter-test-vswitch-rdma.jpg)

1. Установите на узле vNIC метки приоритета, дополняющие предыдущие параметры виртуальной ЛС.

   ```powershell
   Set-VMNetworkAdapter -ManagementOS -Name "MGT" -IeeePriorityTag on
   Get-VMNetworkAdapter -ManagementOS -Name "MGT" | fl Name,IeeePriorityTag
   ```

   _**Результаты**_

   Имя: "центр Ииеприорититаг: вкл."

2. Создайте два узла vNIC для RDMA и подключите их к ВМСТЕСТ vSwitch.

   ```powershell
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB1 –ManagementOS
   Add-VMNetworkAdapter –SwitchName "VMSTEST" –Name SMB2 –ManagementOS
   ```

3. Просмотр свойств сетевого адаптера управления.

   ```powershell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Результаты**_


   |         name         | исманажементос |        VMName        |  SwitchName  | MacAddress | Состояние | IPAddresses |
   |----------------------|----------------|----------------------|--------------|------------|--------|-------------|
   | CORP — внешний коммутатор |      True      | CORP — внешний коммутатор | 001B785768AA |    '    | &nbsp; |             |
   |         Склад          |      True      |       вмстест        | E41D2D074071 |    '    | &nbsp; |             |
   |         SMB1         |      True      |       вмстест        | 00155D30AA00 |    '    | &nbsp; |             |
   |         SMB2         |      True      |       вмстест        | 00155D30AA01 |    '    | &nbsp; |             |

## <a name="step-9-assign-an-ip-address-to-the-smb-host-vnics-vethernet-smb1-and-vethernet-smb2"></a>Шаг 9. Назначьте IP-адрес узлу SMB vNIC адаптера vethernet \( SMB1 \) и адаптера vethernet \( SMB2\)

Для физических адаптеров TEST-40G-1 и TEST-40G-2 по-прежнему настроена локальная виртуальная ЛС 101 и 102. По этой причине адаптеры проверяют трафик и проходят проверку пометок. Ранее вы настроили идентификаторы виртуальной ЛС ПНИК в ноль, а затем настроили ВМСТЕСТ vSwitch на виртуальную ЛС 101. После этого вы по-прежнему можете проверить связь с удаленным адаптером виртуальной ЛС 101 с помощью средства "центр vNIC", но сейчас нет членов VLAN 102.



1. Удалите параметр доступа к виртуальной ЛС из физического сетевого адаптера, чтобы предотвратить автоматическое добавление тегов в исходящий трафик с неверным ИДЕНТИФИКАТОРом виртуальной ЛС и предотвратить фильтрацию входящего трафика, который не соответствует ИДЕНТИФИКАТОРу виртуальной ЛС доступа.

   ```powershell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB1)" -IPAddress 192.168.2.111 -PrefixLength 24
   ```

   _**Результаты**_

   ```
   IPAddress : 192.168.2.111
   InterfaceIndex: 40
   InterfaceAlias: vEthernet (SMB1)
   AddressFamily : IPv4
   Type  : Unicast
   PrefixLength  : 24
   PrefixOrigin  : Manual
   SuffixOrigin  : Manual
   AddressState  : Invalid
   ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   SkipAsSource  : False
   PolicyStore   : PersistentStore
   ```

2. Протестируйте адаптер удаленной виртуальной ЛС 102.

   ```powershell
   Test-NetConnection 192.168.2.5
   ```

   _**Результаты**_

   ```
   ComputerName   : 192.168.2.5
   RemoteAddress  : 192.168.2.5
   InterfaceAlias : vEthernet (SMB1)
   SourceAddress  : 192.168.2.111
   PingSucceeded  : True
   PingReplyDetails (RTT) : 0 ms
   ```

3. Добавьте новый IP-адрес для интерфейса адаптера vethernet \( SMB2 \) .

   ```powershell
   New-NetIPAddress -InterfaceAlias "vEthernet (SMB2)" -IPAddress 192.168.2.222 -PrefixLength 24
   ```

   _**Результаты**_

   ```
   IPAddress : 192.168.2.222
   InterfaceIndex: 44
   InterfaceAlias: vEthernet (SMB2)
   AddressFamily : IPv4
   Type  : Unicast
   PrefixLength  : 24
   PrefixOrigin  : Manual
   SuffixOrigin  : Manual
   AddressState  : Invalid
   ValidLifetime : Infinite ([TimeSpan]::MaxValue)
   PreferredLifetime : Infinite ([TimeSpan]::MaxValue)
   SkipAsSource  : False
   PolicyStore   : PersistentStore
   ```

4. Снова проверьте подключение.


5. Поместите vNIC узла RDMA в уже существующую виртуальную ЛС 102.

   ```powershell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB1" -VlanId "102" -Access -ManagementOS
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName "SMB2" -VlanId "102" -Access -ManagementOS

   Get-VMNetworkAdapterVlan -ManagementOS
   ```

   _**Результаты**_

   ```
   VMName VMNetworkAdapterName Mode VlanList
   ------ -------------------- ---- --------
      SMB1 Access   102
      Mgt  Access   101
      SMB2 Access   102
      CORP-External-Switch Untagged
   ```

6. Проверьте сопоставление SMB1 и SMB2 с базовыми физическими сетевыми адаптерами в группе Team SET vSwitch.<p>Связь узла vNIC с физическими сетевыми адаптерами случайна и подлежит перераспределению при создании и уничтожении. В этом случае можно использовать косвенный механизм для проверки текущей связи. MAC-адреса, связанные с SMB1 и SMB2, связаны с членом группы сетевой карты TESTing – 40G-2. Это не идеальный вариант, так как Test-40G-1 не имеет связанного с ним узла SMB vNIC и не позволяет использовать трафик RDMA по каналу до тех пор, пока не будет сопоставлено с ним узел SMB vNIC.

   ```powershell
   Get-NetAdapterVPort (Preferred)

   Get-NetAdapterVmqQueue
   ```

   _**Результаты**_

   ```
   Name   QueueID MacAddressVlanID Processor VmFriendlyName
   ----   ------- ---------------- --------- --------------
   TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
   TEST-40G-2 1   00-15-5D-30-AA-00 1020:17
   TEST-40G-2 2   00-15-5D-30-AA-01 1020:17
   ```

7. Просмотрите свойства сетевого адаптера виртуальной машины.

   ```powershell
   Get-VMNetworkAdapter -ManagementOS
   ```

   _**Результаты**_

   ```
   Name IsManagementOs VMName SwitchName   MacAddress   Status IPAddresses
   ---- -------------- ------ ----------   ----------   ------ -----------
   CORP-External-Switch True  CORP-External-Switch 001B785768AA {Ok}
   Mgt  True  VMSTEST  E41D2D074071 {Ok}
   SMB1 True  VMSTEST  00155D30AA00 {Ok}
   SMB2 True  VMSTEST  00155D30AA01 {Ok}
   ```

8. Просмотр сопоставления группы сетевых адаптеров.<p>Результаты не должны возвращать сведения, так как сопоставление еще не выполнено.

   ```powershell
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB1
   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName SMB2
   ```


9. Сопоставьте SMB1 и SMB2 с отдельными членами группы физических сетевых адаптеров и просмотрите результаты действий.

   >[!IMPORTANT]
   >Убедитесь, что вы выполнили этот шаг перед продолжением, или сбой вашей реализации.

   ```powershell
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB1" -PhysicalNetAdapterName "Test-40G-1"
   Set-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST -VMNetworkAdapterName "SMB2" -PhysicalNetAdapterName "Test-40G-2"

   Get-VMNetworkAdapterTeamMapping -ManagementOS -SwitchName VMSTEST
   ```

   _**Результаты**_

   ```
   NetAdapterName : Test-40G-1
   NetAdapterDeviceId : {BAA9A00F-A844-4740-AA93-6BD838F8CFBA}
   ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB1'
   IsTemplate : False
   CimSession : CimSession: .
   ComputerName   : 27-3145G0803
   IsDeleted  : False

   NetAdapterName : Test-40G-2
   NetAdapterDeviceId : {B7AB5BB3-8ACB-444B-8B7E-BC882935EBC8}
   ParentAdapter  : VMInternalNetworkAdapter, Name = 'SMB2'
   IsTemplate : False
   CimSession : CimSession: .
   ComputerName   : 27-3145G0803
   IsDeleted  : False
   ```

10. Подтвердите сопоставления MAC, созданные ранее.

    ```powershell
    Get-NetAdapterVmqQueue
    ```

    _**Результаты**_

    ```
    Name   QueueID MacAddressVlanID Processor VmFriendlyName
    ----   ------- ---------------- --------- --------------
    TEST-40G-1 1   E4-1D-2D-07-40-71 1010:17
    TEST-40G-1 2   00-15-5D-30-AA-00 1020:17
    TEST-40G-2 1   00-15-5D-30-AA-01 1020:17
    ```


11. Проверьте подключение из удаленной системы, так как оба узла vNIC находятся в одной подсети и имеют один и тот же ИД виртуальной ЛС \( 102 \) .

    ```powershell
    Test-NetConnection 192.168.2.111
    ```

    _**Результаты**_

    ```
    ComputerName   : 192.168.2.111
    RemoteAddress  : 192.168.2.111
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    ```

    ```powershell
    Test-NetConnection 192.168.2.222
    ```

    _**Результаты**_

    ```
    ComputerName   : 192.168.2.222
    RemoteAddress  : 192.168.2.222
    InterfaceAlias : Test-40G-2
    SourceAddress  : 192.168.2.5
    PingSucceeded  : True
    PingReplyDetails (RTT) : 0 ms
    ```
12. Задайте имя, имя коммутатора и теги приоритета.

    ```powershell
    Set-VMNetworkAdapter -ManagementOS -Name "SMB1" -IeeePriorityTag on
    Set-VMNetworkAdapter -ManagementOS -Name "SMB2" -IeeePriorityTag on
    Get-VMNetworkAdapter -ManagementOS -Name "SMB*" | fl Name,SwitchName,IeeePriorityTag,Status
    ```

    _**Результаты**_

    ```
    Name: SMB1
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}

    Name: SMB2
    SwitchName  : VMSTEST
    IeeePriorityTag : On
    Status  : {Ok}
    ```

13. Просмотрите свойства сетевого адаптера адаптера vethernet.

    ```powershell
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | ft -AutoSize
    ```

    _**Результаты**_

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  False
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  False
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

14. Включите сетевые адаптеры адаптера vethernet.

    ```powershell
    Enable-NetAdapterRdma -Name "vEthernet (SMB1)"
    Enable-NetAdapterRdma -Name "vEthernet (SMB2)"
    Get-NetAdapterRdma -Name "vEthernet*" | sort Name | fl *
    ```

    _**Результаты**_

    ```
    Name  InterfaceDescription Enabled
    ----  -------------------- -------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  True
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  True
    vEthernet (MGT)   Hyper-V Virtual Ethernet Adapter #2  False
    ```

## <a name="step-10-validate-the-rdma-functionality"></a>Шаг 10. Проверка функции RDMA

Необходимо проверить функциональность RDMA с удаленной системы на локальную систему, которая имеет vSwitch, для обоих членов команды Team SET vSwitch.<p>Так как узлы vNIC \( SMB1 и SMB2 \) НАЗНАЧАЮТСЯ виртуальной ЛС 102, можно выбрать адаптер VLAN 102 в удаленной системе. <p>В этом примере сетевая карта Test-40G-2 поддерживает RDMA для SMB1 (192.168.2.111) и SMB2 (192.168.2.222).

>[!TIP]
>Возможно, потребуется отключить брандмауэр в этой системе.  Дополнительные сведения см. в политике структуры.
>
>```powershell
>Set-NetFirewallProfile -All -Enabled False
>
>Get-NetAdapterAdvancedProperty -Name "Test-40G-2"
>```
>
>_**Результаты**_
>
>```
>Name  DisplayNameDisplayValue   RegistryKeyword RegistryValue
>----  -----------------------   --------------- -------------
> .
> .
>Test-40G-2VLAN ID102VlanID  {102}
>```

1. Просмотр свойств сетевого адаптера.

   ```powershell
   Get-NetAdapter
   ```

   _**Результаты**_

   ```
   Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
   ----  --------------------------- ------   ---------- ---------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet A...#3   3 Up   E4-1D-2D-07-43-D140 Gbps
   ```

2. Просмотрите сведения о RDMA сетевого адаптера.

   ```powershell
   Get-NetAdapterRdma
   ```

   _**Результаты**_

   ```
   Name  InterfaceDescription Enabled
   ----  -------------------- -------
   Test-40G-2Mellanox ConnectX-3 Pro Ethernet Adap... True
   ```

3. Выполните проверку трафика RDMA на первом физическом адаптере.

   ```powershell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.111 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Результаты**_

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter Test-40G-2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.111, is reachable.
   VERBOSE: Remote IP 192.168.2.111 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 34251744 RDMA bytes sent per second
   VERBOSE: 967346308 RDMA bytes written per second
   VERBOSE: 35698177 RDMA bytes sent per second
   VERBOSE: 976601842 RDMA bytes written per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.111
   ```

4. Выполните проверку трафика RDMA на втором физическом адаптере.

   ```powershell
   C:\TEST\Test-RDMA.PS1 -IfIndex 3 -IsRoCE $true -RemoteIpAddress 192.168.2.222 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Результаты**_

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter Test-40G-2 is a physical adapter
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.222, is reachable.
   VERBOSE: Remote IP 192.168.2.222 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 485137693 RDMA bytes written per second
   VERBOSE: 35200268 RDMA bytes sent per second
   VERBOSE: 939044611 RDMA bytes written per second
   VERBOSE: 34880901 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.222
   ```

5. Проверьте трафик RDMA с локального компьютера на удаленный компьютер.

    ```powershell
    Get-NetAdapter | ft –AutoSize
    ```

    _**Результаты**_

    ```
    Name  InterfaceDescriptionifIndex Status   MacAddress LinkSpeed
    ----  --------------------------- ------   ---------- ---------
    vEthernet (SMB2)  Hyper-V Virtual Ethernet Adapter #4  45 Up   00-15-5D-30-AA-0380 Gbps
    vEthernet (SMB1)  Hyper-V Virtual Ethernet Adapter #3  41 Up   00-15-5D-30-AA-0280 Gbps
    ```

6. Выполните проверку трафика RDMA на первом виртуальном адаптере.

   ```
   C:\TEST\Test-RDMA.PS1 -IfIndex 41 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Результаты**_

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter vEthernet (SMB1) is a virtual adapter
   VERBOSE: Retrieving vSwitch bound to the virtual adapter
   VERBOSE: Found vSwitch: VMSTEST
   VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
   VERBOSE: Remote IP 192.168.2.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 15250197 RDMA bytes sent per second
   VERBOSE: 896320913 RDMA bytes written per second
   VERBOSE: 33947559 RDMA bytes sent per second
   VERBOSE: 912160540 RDMA bytes written per second
   VERBOSE: 34091930 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
   ```

7. Выполните проверку трафика RDMA на втором виртуальном адаптере.

   ```powershell
   C:\TEST\Test-RDMA.PS1 -IfIndex 45 -IsRoCE $true -RemoteIpAddress 192.168.2.5 -PathToDiskspd C:\TEST\Diskspd-v2.0.17\amd64fre\
   ```

   _**Результаты**_

   ```
   VERBOSE: Diskspd.exe found at C:\TEST\Diskspd-v2.0.17\amd64fre\diskspd.exe
   VERBOSE: The adapter vEthernet (SMB2) is a virtual adapter
   VERBOSE: Retrieving vSwitch bound to the virtual adapter
   VERBOSE: Found vSwitch: VMSTEST
   VERBOSE: Found the following physical adapter(s) bound to vSwitch: TEST-40G-1, TEST-40G-2
   VERBOSE: Underlying adapter is RoCE. Checking if QoS/DCB/PFC is configured on each physical adapter(s)
   VERBOSE: QoS/DCB/PFC configuration is correct.
   VERBOSE: RDMA configuration is correct.
   VERBOSE: Checking if remote IP address, 192.168.2.5, is reachable.
   VERBOSE: Remote IP 192.168.2.5 is reachable.
   VERBOSE: Disabling RDMA on adapters that are not part of this test. RDMA will be enabled on them later.
   VERBOSE: Testing RDMA traffic now for. Traffic will be sent in a parallel job. Job details:
   VERBOSE: 0 RDMA bytes written per second
   VERBOSE: 0 RDMA bytes sent per second
   VERBOSE: 385169487 RDMA bytes written per second
   VERBOSE: 33902277 RDMA bytes sent per second
   VERBOSE: 907354685 RDMA bytes written per second
   VERBOSE: 33923662 RDMA bytes sent per second
   VERBOSE: Enabling RDMA on adapters that are not part of this test. RDMA was disabled on them prior to sending RDMA traffic.
   VERBOSE: RDMA traffic test SUCCESSFUL: RDMA traffic was sent to 192.168.2.5
   ```

В последней строке выходных данных "Проверка трафика RDMA успешно выполнена: трафик RDMA, отправленный в 192.168.2.5", показывает, что в адаптере успешно настроены согласованные сетевые адаптеры.

## <a name="related-topics"></a>Связанные темы

- [Конфигурация с согласованным СЕТЕВЫМ адаптером с одним сетевым адаптером](cnic-single.md)
- [Конфигурация физического коммутатора для Объединенных сетевых адаптеров](cnic-app-switch-config.md)
- [Устранение неполадок конфигураций Объединенных сетевых адаптеров](cnic-app-troubleshoot.md)
