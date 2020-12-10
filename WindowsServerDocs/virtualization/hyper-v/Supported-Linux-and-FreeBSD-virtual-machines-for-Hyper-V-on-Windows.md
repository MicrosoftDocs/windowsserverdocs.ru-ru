---
title: Поддерживаемые виртуальные машины Linux и FreeBSD для Hyper-V в Windows
description: Список служб и компонентов интеграции Linux, входящих в каждую версию
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
ms.author: benarm
author: BenjaminArmstrong
ms.date: 12/09/2020
ms.openlocfilehash: 1eeb5a80d0f08a158f0052fb1ba69d2adacf0b4d
ms.sourcegitcommit: f95a991491ff09260d979078e248e2636bd2db54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "96997811"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Поддерживаемые виртуальные машины Linux и FreeBSD для Hyper-V в Windows

>Применимо к: Azure Stack ХЦИ, версия 20H2; Windows Server 2019, Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012, Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7,1, Windows 7

Hyper-V поддерживает как эмулированные, так и устройства Hyper-V для виртуальных машин Linux и FreeBSD. При работе с имитируемыми устройствами не требуется устанавливать дополнительное программное обеспечение. Однако эмулированные устройства не обеспечивают высокую производительность и не могут использовать обширную инфраструктуру управления виртуальными машинами, предлагаемую технологией Hyper-V. Чтобы полностью использовать все преимущества, предоставляемые Hyper-V, лучше всего использовать устройства, относящиеся к Hyper-V, для Linux и FreeBSD. Коллекция драйверов, необходимых для запуска устройств, связанных с Hyper-V, известна как Linux Integration Services (LIS) или FreeBSD Integration Services (BIS).

LIS был добавлен в ядро Linux и обновлен для новых выпусков. Однако дистрибутивы Linux, основанные на старых ядрах, могут не иметь последних улучшений или исправлений. Корпорация Майкрософт предоставляет загружаемый пакет, содержащий устанавливаемые драйверы LIS для некоторых установок Linux на основе этих старых ядер. Поскольку поставщики распространения включают версии Linux Integration Services, лучше установить последнюю загружаемую версию LIS, если это применимо, для установки.

Для других дистрибутивов Linux изменения LIS регулярно интегрируются в ядро операционной системы и приложения, поэтому отдельное скачивание или установка не требуются.

Для старых выпусков FreeBSD (до 10,0) корпорация Майкрософт предоставляет порты, которые содержат устанавливаемые драйверы BIS и соответствующие управляющие программы для виртуальных машин FreeBSD. Для новых выпусков FreeBSD номер BIS встроен в операционную систему FreeBSD, и отдельное скачивание или установка не требуются, за исключением загрузки KVP портов, необходимой для FreeBSD 10,0.

> [!TIP]
> - Загрузите [Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) из центра оценки.

Целью этого содержимого является предоставление информации, помогающей упростить развертывание Linux или FreeBSD в Hyper-V. Ниже приведены конкретные сведения.

* Дистрибутивы Linux или выпуски FreeBSD, требующие загрузки и установки драйверов LIS или BIS.

* Дистрибутивы Linux или выпуски FreeBSD, содержащие встроенные драйверы LIS или BIS.

* Карты распределения компонентов, которые указывают на функции в основных дистрибутивах Linux или в выпусках FreeBSD.

* Известные проблемы и способы их решения для каждого распространения или выпуска.

* Описание функции для каждого компонента LIS или BIS.

**Хотите принять предложение о функциях и функциях?** Что мы можем сделать лучше? Вы можете использовать веб-сайт [пользователя Windows Server](https://windowsserver.uservoice.com/forums/295062-linux-support) , чтобы предложить новые функции и возможности для виртуальных машин Linux и FreeBSD в Hyper-V, а также узнать, какие другие люди говорят.

## <a name="in-this-section"></a>В этом разделе

* [Поддерживаемые CentOS и Red Hat Enterprise Linux виртуальные машины в Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Debian в Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Oracle Linux в Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины SUSE в Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Ubuntu в Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины FreeBSD в Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Описания функций для виртуальных машин Linux и FreeBSD в Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Рекомендации по запуску Linux в Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Рекомендации по запуску FreeBSD в Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
