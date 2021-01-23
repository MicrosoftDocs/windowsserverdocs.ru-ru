---
title: Новые возможности виртуализации сети Hyper-V в Windows Server 2016
description: В этом разделе содержатся сведения о новых возможностях виртуализации сети Hyper-V в Windows Server 2016.
manager: grcusanz
ms.topic: article
ms.assetid: 0254275a-0a77-40a9-b68a-1029284c03fe
ms.author: anpaul
author: AnirbanPaul
ms.date: 03/19/2018
ms.openlocfilehash: ceab0e8ea517eb8fa992ec7f41010e9f14bb38bb
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716920"
---
# <a name="whats-new-in-hyper-v-network-virtualization-in-windows-server-2016"></a>Новые возможности виртуализации сети Hyper-V в Windows Server 2016

>Применяется к: Windows Server 2019, Windows Server 2016

В этом разделе описывается новая или измененная функция виртуализации сети Hyper-V (HNV) в Windows Server 2016.

## <a name="updates-in-hnv"></a><a name="BKMK_IPAM2012R2"></a>Обновления в HNV
HNV предлагает расширенную поддержку в следующих областях:

|Компонент или функциональная возможность|Новая или улучшенная|Описание|
|--------------------------|-------------------|---------------|
|[Программируемый коммутатор Hyper-V](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SDN)|Оператор new|Политика HNV может быть программируемой через сетевой контроллер (Майкрософт).|
|[Поддержка инкапсуляции ВКСЛАН](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#VXLAN)|Оператор new|HNV теперь поддерживает инкапсуляцию ВКСЛАН.|
|[Взаимодействие Load Balancer программного обеспечения (SLB)](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#SLB)|Оператор new|HNV полностью интегрирован с программным обеспечением Майкрософт Load Balancer.|
|[Соответствующие заголовки IEEE Ethernet](../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/../../../sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md#L2)|Улучшена команда|Соответствует стандартам IEEE Ethernet|

### <a name="programmable-hyper-v-switch"></a><a name="SDN"></a>Программируемый коммутатор Hyper-V
HNV — это фундаментальный строитель обновленного программного обеспечения (SDN) корпорации Майкрософт, который полностью интегрирован в стек SDN.

Новый сетевой контроллер Майкрософт отправляет политики HNV в агент узла, работающий на каждом узле, используя открытый протокол управления vSwitch (ОВСДБ) в качестве интерфейса Подсистемамми (ЛИКВИДНЫЙ SBI). Агент узла сохраняет эту политику, используя настройку [схемы втеп](https://github.com/openvswitch/ovs/blob/master/vtep/vtep.ovsschema) и программирует сложные правила потока в подсистему обработки потока в коммутаторе Hyper-V.

Подсистема обработки потока в коммутаторе Hyper-V является тем же механизмом, который используется в Microsoft Azure &trade; , который был проверен на уровне Hyper-Scale в Microsoft Azure общедоступном облаке. Кроме того, все стеки SDN по отношению к сетевому контроллеру и поставщику сетевых ресурсов (см. в ближайшее время) согласуются с Microsoft Azure, тем самым обеспечивая мощь Microsoft Azure общедоступного облака для наших предприятий и поставщиков услуг хостинга.

> [!NOTE]
> Дополнительные сведения о ОВСДБ см. в [документе RFC 7047](https://www.rfc-editor.org/info/rfc7047).

Коммутатор Hyper-V поддерживает правила потока без отслеживания состояния и с отслеживанием состояния на основе простого действия "сопоставление" в подсистеме обработки потока Майкрософт.

![Коммутатор Hyper-V Windows Server 2016](../../../media/what-s-new-in-hyper-v-network-virtualization-in-windows-server/HNVOverview.png)

### <a name="vxlan-encapsulation-support"></a><a name="VXLAN"></a>Поддержка инкапсуляции ВКСЛАН
Виртуальный расширяемый протокол расширенной локальной сети (ВКСЛАН- [RFC 7348](https://www.rfc-editor.org/info/rfc7348)) широко распространен на рынке, благодаря поддержке от таких поставщиков, как Cisco, вооруженный, Dell, HP и др. Кроме того, HNV теперь поддерживает эту схему инкапсуляции с использованием режима распространения MAC через сетевой контроллер Майкрософт для сопоставления программ IP-адресам сети наложения клиентов (адрес клиента или ЦС) физическим IP-адресам ундерлай сети (адрес поставщика или PA). Разгрузки задач NVGRE и ВКСЛАН поддерживаются для повышения производительности с помощью драйверов сторонних производителей.

### <a name="software-load-balancer-slb-interoperability"></a><a name="SLB"></a>Взаимодействие Load Balancer программного обеспечения (SLB)
Windows Server 2016 включает в себя программную подсистему балансировки нагрузки с полной поддержкой трафика виртуальной сети и беспрепятственного взаимодействия с HNV. SLB реализуется с помощью подсистемы выполнения потоков в коммутаторе плоскости данных v-Switch и контролируется сетевым контроллером для сопоставлений виртуальных IP-адресов и динамических IP-адресов (DIP).

### <a name="compliant-ieee-ethernet-headers"></a><a name="L2"></a>Соответствующие заголовки IEEE Ethernet
HNV реализует правильные заголовки Ethernet уровня L2 для обеспечения взаимодействия с виртуальными и физическими устройствами сторонних производителей, которые зависят от стандартных отраслевых протоколов. Корпорация Майкрософт гарантирует, что все передаваемые пакеты имеют соответствующие значения во всех полях, чтобы обеспечить это взаимодействие. Кроме того, поддержка крупных кадров (MTU > 1780) в физической сети L2 должна учитывать служебные расходы на пакеты, представленные протоколами инкапсуляции (NVGRE, ВКСЛАН), и гарантирует, что Гостевые виртуальные машины, подключенные к виртуальной сети HNV, обслуживают 1514 MTU.

## <a name="additional-references"></a>Дополнительные ссылки

-   [Обзор виртуализации сети Hyper-V](hyperv-network-virtualization-overview-windows-server.md)

-   [Технический обзор виртуализации сети Hyper-V](hyperv-network-virtualization-technical-details-windows-server.md)

-   [Программно-конфигурируемая сеть](../../software-defined-networking.md)