---
title: Рекомендации по запуску FreeBSD в Hyper-V
description: Содержит рекомендации по запуску FreeBSD на виртуальных машинах.
ms.topic: article
ms.assetid: 0c66f1c8-2606-43a3-b4cc-166acaaf2d2a
ms.author: benarm
author: BenjaminArmstrong
ms.date: 01/09/2017
ms.openlocfilehash: 09b6f532bac2b57fd8334556501c6197fa3036cc
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747159"
---
# <a name="best-practices-for-running-freebsd-on-hyper-v"></a>Рекомендации по запуску FreeBSD в Hyper-V

>Область применения: Windows Server 2019, Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012, Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

В этом разделе содержится список рекомендаций по запуску FreeBSD в качестве гостевой операционной системы на виртуальной машине Hyper-V.

## <a name="enable-carp-in-freebsd-102-on-hyper-v"></a>Включение CARP в FreeBSD 10,2 в Hyper-V

Протокол CARP позволяет нескольким узлам использовать один и тот же IP-адрес и идентификатор виртуального узла (ВХИД), чтобы обеспечить высокий уровень доступности для одной или нескольких служб. В случае сбоя одного или нескольких узлов другие узлы прозрачно перейдут, чтобы пользователи не могли заметить сбой службы. Чтобы использовать CARP в FreeBSD 10,2, следуйте инструкциям в руководстве по [FreeBSD](https://www.freebsd.org/doc/en/books/handbook/carp.html) и выполните следующие действия в диспетчере Hyper-V.

* Убедитесь, что виртуальная машина имеет сетевой адаптер, и ей назначен виртуальный коммутатор. Выберите виртуальную машину и щелкните **Actions**  >  **Параметры**действия.

![Снимок экрана параметров виртуальной машины с выбранным сетевым адаптером](media/Hyper-V_Settings_NetworkAdapter.png)

* Включите подмену MAC-адресов. Для этого сделайте следующее.

   1. Выберите виртуальную машину и щелкните **Actions**  >  **Параметры**действия.

   2. Разверните узел **сетевой адаптер** и выберите **Дополнительные функции**.

   3. Выберите **включить подмену MAC-адресов**.

## <a name="create-labels-for-disk-devices"></a>Создание меток для дисковых устройств

Во время запуска узлы устройств создаются при обнаружении новых устройств. Это может означать, что имена устройств могут измениться при добавлении новых устройств. Если во время запуска возникает ошибка КОРНЕВого подключения, необходимо создать метки для каждой секции IDE, чтобы избежать конфликтов и изменений. Дополнительные сведения см. в разделе [маркировка дисковых устройств](https://www.freebsd.org/doc/handbook/geom-glabel.html). Ниже приведены примеры.

> [!IMPORTANT]
> Создайте резервную копию fstab, прежде чем вносить изменения.

1. Перезагрузите систему в однопользовательском режиме. Это можно сделать, выбрав в меню загрузки пункт 2 для FreeBSD 10.3 + (вариант 4 для FreeBSD 8. x) или выполнив команду boot-s из командной строки.

2. В однопользовательском режиме Создайте метки ЖЕОМ для каждого раздела диска IDE, указанного в fstab (корневой и подкачки). Ниже приведен пример FreeBSD 10,3.

   ```bash
   # cat  /etc/fstab
   # Device           Mountpoint      FStype  Options   Dump   Pass#
   /dev/da0p2         /               ufs     rw        1       1
   /dev/da0p3         none            swap    sw        0       0

   # glabel  label rootfs  /dev/da0p2
   # glabel  label swap   /dev/da0p3
   # exit
   ```

   Дополнительные сведения о метках ЖЕОМ можно найти по адресу: Добавление [меток для дисковых устройств](https://www.freebsd.org/doc/handbook/geom-glabel.html).

3. Система продолжит загрузку нескольких пользователей. После завершения загрузки измените/etc/fstab и замените имена стандартных устройств соответствующими метками. Окончательный/etc/fstab будет выглядеть следующим образом:

   ```
   # Device                Mountpoint      FStype  Options         Dump    Pass#
   /dev/label/rootfs       /               ufs     rw              1       1
   /dev/label/swap         none            swap    sw              0       0
   ```

4. Теперь система может быть перезагружена. Если все прошло хорошо, в обычном режиме будет отображаться следующее:

   ```
   # mount
   /dev/label/rootfs on / (ufs, local, journaled soft-updates)
   devfs on /dev (devfs, local, mutilabel)
   ```

## <a name="use-a-wireless-network-adapter-as-the-virtual-switch"></a>Использование беспроводного сетевого адаптера в качестве виртуального коммутатора

Если виртуальный коммутатор на узле основан на адаптере беспроводной сети, уменьшите срок действия ARP до 60 секунд, выполнив следующую команду. В противном случае сетевые подключения виртуальной машины могут перестанут работать через некоторое время.


```
   # sysctl net.link.ether.inet.max_age=60
```


См. также

* [Поддерживаемые виртуальные машины FreeBSD в Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)
