---
title: Основы DHCP (протокол динамического конфигурирования узлов)
description: 'Дополнительные сведения: основные сведения о DHCP (протокол динамической конфигурации узлов)'
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: troubleshooting
author: Deland-Han
ms.author: delhan
ms.reviewer: ''
ms.openlocfilehash: e86fd0e520a526357737094e152b3aa2c4f58621
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948570"
---
# <a name="dhcp-dynamic-host-configuration-protocol-basics"></a>Основы DHCP (протокол динамического конфигурирования узлов)

Протокол DHCP — это стандартный протокол, определяемый RFC 1541 (который заменяется RFC 2131), позволяющий серверу динамически распределять IP-адреса и сведения о конфигурации клиентам. Как правило, DHCP-сервер предоставляет клиенту по крайней мере следующие основные сведения:

- IP-адрес

- Маска подсети

- Также могут быть предоставлены сведения о Гатевайосер по умолчанию, такие как адреса серверов службы доменных имен (DNS) и адреса серверов WINS. Системный администратор настраивает DHCP-сервер с параметрами, которые анализируются на клиенте.

## <a name="more-information"></a>Дополнительные сведения

Функции DHCP-клиента предоставляются в следующих продуктах Майкрософт:

- Windows NT Server версии 3,5, 3,51 и 4,0

- Windows NT Workstation версии 3,5, 3,51 и 4,0

- Windows 95

- Microsoft Network Client версии 3,0 для MS-DOS

- Клиент Microsoft LAN Manager версии 2.2 c для MS-DOS

- Microsoft TCP/IP-32 для Windows для рабочих групп версии 3,11, 3.11 a и 3.11 b

Разные DHCP-клиенты поддерживают различные параметры, которые они могут получить от DHCP-сервера.

Следующие операционные системы Microsoft Server предоставляют функции DHCP-сервера:

- Windows NT Server версии 3,5

- Windows NT Server версии 3,51

- Windows NT Server версии 4,0

Когда клиент инициализируется в первый раз после настройки на получение данных DHCP, он инициирует диалог с сервером.

Ниже приведена сводная таблица диалога между клиентом и сервером, за которой следует описание процесса на уровне пакета:

```
Source Dest Source Dest Packet
 MAC addr MAC addr IP addr IP addr Description
 -----------------------------------------------------------------
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Discover
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP Offer
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Request
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP ACK
```

Ниже приведен подробный диалог между клиентом DHCP и DHCP-сервером.

### <a name="dhcpdiscover"></a>DHCPDISCOVER

Клиент отправляет пакет DHCPDISCOVER. Ниже приведен фрагмент записи сетевого монитора, в которой показаны IP-и DHCP-части пакета DHCPDISCOVER. В разделе IP-адреса можно увидеть адрес назначения 255.255.255.255, а исходный адрес — 0.0.0.0. Раздел DHCP идентифицирует пакет как пакет обнаружения и идентифицирует клиент в двух местах, используя физический адрес сетевой карты. Обратите внимание, что значения в полях ЧАДДР и DHCP: Client identifier идентичны.

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpoffer"></a>дхкпоффер

DHCP-сервер отвечает, отправляя пакет ДХКПОФФЕР. В разделе IP фрагмента записи ниже исходный адрес теперь является IP-адресом сервера DHCP, а адресом назначения является широковещательный адрес 255.255.255.255. Раздел DHCP определяет пакет как предложение. Поле ИАДДР заполняется IP-адресом, который сервер предлагает клиенту. Обратите внимание, что поле ЧАДДР по-прежнему содержит физический адрес запрашивающего клиента. Кроме того, в разделе поля параметров DHCP можно найти различные параметры, отправляемые сервером вместе с IP-адресом. В этом случае сервер отправляет маску подсети, шлюз по умолчанию (маршрутизатор), время аренды, адрес WINS-сервера (служба имен NetBIOS) и тип узла NetBIOS.

```

IP: ID = 0x3C30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15408 (0x3C30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2FA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Offer (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Offer
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

### <a name="dhcprequest"></a>DHCPREQUEST

Клиент отвечает на ДХКПОФФЕР, отправляя DHCPREQUEST. В разделе IP-адресов записи ниже исходный адрес клиента по-прежнему равен 0.0.0.0, а место назначения пакета по-прежнему 255.255.255.255. Клиент оставляет 0.0.0.0, так как клиент не получал проверку с сервера, что его можно использовать в предложенном адресе. Назначением по-прежнему выполняется вещание, так как может быть получен ответ от нескольких DHCP-серверов и может храниться резервирование для предложения, сделанного клиентом. Это позволяет другим DHCP-серверам понять, что они могут освободить свои предложенные адреса и вернуть их в доступные пулы. Раздел DHCP идентифицирует пакет как запрос и проверяет предложенный адрес с помощью поля DHCP: запрошенный адрес. В поле Идентификатор сервера DHCP: отображается IP-адрес DHCP-сервера, предоставляющего аренду.

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpack"></a>ТРАНСЛИРУЕТ

DHCP-сервер отвечает на DHCPREQUEST с помощью DHCPACK, тем самым завершая цикл инициализации. Исходный адрес — это IP-адрес сервера DHCP, а адрес назначения по-прежнему — 255.255.255.255. Поле ИАДДР содержит адрес клиента, а поля ЧАДДР и DHCP: Client identifier являются физическим адресом сетевой карты в запрашивающем клиенте. Раздел параметров DHCP определяет пакет как подтверждение.

```

IP: ID = 0x3D30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15664 (0x3D30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2EA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: ACK (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP ACK
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

Если у клиента ранее был назначен IP-адрес DHCP и он перезапущен, клиент будет запрашивать ранее арендованный IP-адрес в специальном пакете DHCPREQUEST. Адрес источника — 0.0.0.0, а местом назначения — широковещательный адрес 255.255.255.255. Клиенты Майкрософт заполнят поле параметра DHCP DHCP: запрошенный адрес с ранее назначенным адресом. Строго совместимые с RFC клиенты заполняют поле ЦИАДДР с запрошенным адресом. Сервер Microsoft DHCP будет принимать либо.

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=2757554E)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 660034894 (0x2757554E)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

На этом этапе сервер может не отвечать на запросы. Поведение DHCP-сервера Windows NT зависит от используемой версии операционной системы, а также от других факторов, таких как ограничение области. Если сервер определяет, что клиент по-прежнему может использовать этот адрес, он будет либо в автоматическом режиме, либо на подтверждение DHCPREQUEST. Если сервер определяет, что у клиента не может быть адреса, он будет передавать НАКК.

```

IP: ID = 0x3F1A; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 16154 (0x3F1A)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2CBE
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: NACK (xid=74A005CE)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1956644302 (0x74A005CE)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP NACK
 DHCP: Server Identifier = 157.54.48.151
 DHCP: End of this option field

```

После этого клиент начнет процесс обнаружения, но пакет DHCPDISCOVER по-прежнему будет пытаться арендовать тот же адрес. Во многих случаях клиент ТС получает один и тот же адрес, но не может.

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=3ED14752)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1053902674 (0x3ED14752)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.51.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

Сведения о DHCP, получаемые клиентом с DHCP-сервера, будут связаны со временем аренды. Время аренды определяет, как долго клиент может использовать сведения, назначенные службой DHCP. Когда аренда достигает определенных вех, клиент попытается обновить свои данные DHCP.

Для просмотра сведений о IP-адресе в клиенте Windows или Windows для рабочих групп используйте служебную программу IPCONFIG. Если клиент является Windows 95, используйте WINIPCFG.

## <a name="references"></a>Ссылки

Дополнительные сведения о DHCP см. в разделе RFC1541 и RFC2131. Документы RFC могут быть получены через Интернет на многочисленных сайтах, например: [http://www.rfc-editor.org/](http://www.rfc-editor.org/) и [http://www.tech-nic.qc.ca/](http://www.tech-nic.qc.ca/)
