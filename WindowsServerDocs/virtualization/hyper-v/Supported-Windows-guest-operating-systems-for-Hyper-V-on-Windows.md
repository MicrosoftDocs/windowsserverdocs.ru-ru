---
title: Поддерживаемые гостевые операционные системы Windows для Hyper-V в Windows Server
description: Список операционных систем Windows, поддерживаемых для использования в качестве гостя на виртуальной машине. Также содержит ссылки на похожие статьи для предыдущих версий Hyper-V.
ms.topic: article
ms.assetid: 06b35897-2192-48b7-8c2d-125c520b0786
ms.author: benarm
author: BenjaminArmstrong
ms.date: 01/08/2019
ms.openlocfilehash: 2e5cf6c94d0127a283c640a48aaa2fced5472e9d
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746729"
---
# <a name="supported-windows-guest-operating-systems-for-hyper-v-on-windows-server"></a>Поддерживаемые гостевые операционные системы Windows для Hyper-V в Windows Server

>Область применения. Windows Server 2016, Windows Server 2019

Hyper-V поддерживает несколько версий дистрибутивов Windows Server, Windows и Linux для работы на виртуальных машинах в качестве гостевых операционных систем. В этой статье рассматриваются поддерживаемые операционные системы Windows Server и гостевые ОС Windows. Сведения о дистрибутивах Linux и FreeBSD см. [в статье Поддерживаемые виртуальные машины Linux и FreeBSD для Hyper-V в Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).

Некоторые операционные системы имеют встроенные службы Integration Services. Для других требуется установить или обновить службы Integration Services как отдельный шаг после настройки операционной системы на виртуальной машине. Дополнительные сведения см. в разделах ниже и  [Integration Services](/virtualization/hyper-v-on-windows/reference/integration-services).

## <a name="supported-windows-server-guest-operating-systems"></a>Поддерживаемые гостевые операционные системы Windows Server

Ниже приведены версии Windows Server, которые поддерживаются в качестве гостевых операционных систем для Hyper-V в Windows Server 2016 и Windows Server 2019.

|Операционная система на виртуальной машине (сервер)|Максимальное число виртуальных процессоров.|Службы Integration Services|Примечания|
|-------------------------------------|----------------------------------------|------------------------|---------|
|Windows Server, версия 1909 |240 для поколения 2;<br>64 для поколения 1|Встроено|Для поддержки более 240 виртуальных процессоров требуется Windows Server, версия 1903 или более поздняя гостевая операционная система.|
|Windows Server версии 1903 |240 для поколения 2;<br>64 для поколения 1|Встроено||
|Windows Server, версия 1809 |240 для поколения 2;<br>64 для поколения 1|Встроено||
|Windows Server 2019 |240 для поколения 2;<br>64 для поколения 1|Встроено||
|Windows Server, версия 1803 |240 для поколения 2;<br>64 для поколения 1|Встроено||
|Windows Server 2016 |240 для поколения 2;<br>64 для поколения 1|Встроено||
|Windows Server 2012 R2 |64|Встроено||
|Windows Server 2012 |64|Встроено||
|Windows Server 2008 R2 с пакетом обновления 1 (SP1)|64|Установите все критические обновления Windows после настройки операционной системы на виртуальной машине.|Выпуски Datacenter, Enterprise, Standard и Web.|
|Windows Server 2008 с пакетом обновления 2 (SP2)|8|Установите все критические обновления Windows после настройки операционной системы на виртуальной машине.|Выпуски Datacenter, Enterprise, Standard и Web (32-разрядные и 64-разрядные).|

## <a name="supported-windows-client-guest-operating-systems"></a>Поддерживаемые гостевые операционные системы клиента Windows

Ниже приведены версии клиента Windows, которые поддерживаются в качестве гостевых операционных систем для Hyper-V в Windows Server 2016 и Windows Server 2019.

|Операционная система на виртуальной машине (клиент)|Максимальное число виртуальных процессоров.|Службы Integration Services|Примечания|
|-------------------------------------|----------------------------------------|------------------------|---------|
|Windows 10|32|Встроено||
|Windows 8.1|32|Встроено||
|Windows 7 с пакетом обновления 1 (SP1)|4|Обновите службы Integration Services после настройки операционной системы на виртуальной машине.|Выпуски Максимальная, Корпоративная и Профессиональная (32-разрядные и 64-разрядные).|

## <a name="guest-operating-system-support-on-other-versions-of-windows"></a>Поддержка гостевых операционных систем в других версиях Windows

В следующей таблице приведены ссылки на сведения о гостевых операционных системах, поддерживаемых Hyper-V, в других версиях Windows.

|Главная операционная система|Раздел|
|-------------------------|---------|
|Windows 10|[Поддерживаемые гостевые операционные системы для клиента Hyper-V в Windows 10](/virtualization/hyper-v-on-windows/about/supported-guest-os)|
|Windows Server 2012 R2 и Windows 8.1|-   [Поддерживаемые гостевые операционные системы Windows для Hyper-V в Windows Server 2012 R2 и Windows 8.1](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792027(v=ws.11))<br />-   [Виртуальные машины Linux и FreeBSD в Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)|
|Windows Server 2012 и Windows 8|[Поддерживаемые операционные системы Windows на виртуальных машинах для Hyper-V в Windows Server 2012 и Windows 8](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792028(v=ws.11))|
|Windows Server 2008 и Windows Server 2008 R2|[О виртуальных машинах и гостевых операционных системах](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc794868(v=ws.10))|

## <a name="how-microsoft-provides-support-for-guest-operating-systems"></a>Как корпорация Майкрософт обеспечивает поддержку гостевых операционных систем

Корпорация Майкрософт обеспечивает поддержку гостевых операционных систем следующим образом:

-   Устранение проблем, обнаруженных в операционных системах Майкрософт и в службах интеграции, поддерживается службой технической поддержки Майкрософт.

-   Поддержка по проблемам в других операционных системах, сертифицированных поставщиком операционной системы для выполнения в Hyper-V, обеспечивается поставщиком.

-   Если обнаруживаются проблемы в других операционных системах, корпорация Майкрософт отправляет описание проблемы в сообщество поддержки разных поставщиков [TSANet](https://www.tsanet.org/).

## <a name="additional-references"></a>Дополнительные ссылки

-   [Supported Linux and FreeBSD virtual machines for Hyper-V on Windows](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md) (Поддерживаемые виртуальные машины Linux и FreeBSD для Hyper-V в Windos).

-   [Поддерживаемые гостевые операционные системы для клиента Hyper-V в Windows 10](/virtualization/hyper-v-on-windows/about/supported-guest-os)