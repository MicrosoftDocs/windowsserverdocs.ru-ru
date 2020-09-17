---
title: Поддерживаемые виртуальные машины Oracle Linux в Hyper-V
description: Список служб и компонентов интеграции Linux, входящих в каждую версию
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
ms.author: benarm
author: BenjaminArmstrong
ms.date: 06/05/2020
ms.openlocfilehash: 7c1029f31abe70b09bddc83f928ee492be18ef2b
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746399"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Поддерживаемые виртуальные машины Oracle Linux в Hyper-V

>Область применения: Windows Server 2019, Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows 10, Windows 8.1

Следующая схема распределения признаков показывает функции, которые имеются в каждой версии. Известные проблемы и способы их решения для каждого распространения перечислены после таблицы.

Содержание

* [Серия Oracle Linux 8. x](#oracle-linux-8x-series)
* [Серия Oracle Linux 7. x](#oracle-linux-7x-series)
* [Серия Oracle Linux 6. x](#oracle-linux-6x-series)


## <a name="table-legend"></a>Условные обозначения таблицы

* **Встроенные в** систему LIS включены в состав этого дистрибутива Linux. Номера версий модулей ядра для встроенных LIS (например, как показано в **лсмод**) отличаются от номера версии в пакете скачанных пакетов LIS, предоставленных корпорацией Майкрософт. Несоответствие не означает, что встроенное в LIS Обновление устарело.

* &#10004;-доступный компонент
* (*пусто*) — функция недоступна
* **RHCK** — ядро с совместимостью Red Hat
* **UEK** — неразрывный корпоративный ядра (UEK)
   * UEK4-построено на основе вышестоящего выпуска Linux ядра 4.1.12
   * UEK5-построено на основе вышестоящего выпуска Linux ядра 4,14
   * UEK6-построено на основе вышестоящего выпуска Linux ядра 5,4

## <a name="oracle-linux-8x-series"></a>Серия Oracle Linux 8. x

|       **Компонент**     |       **Версия Windows Server**      |       **8.0 – 8.1 (RHCK)** |
|-----------------------|---------------------------------------|-------------------|
|       **Доступность**        |   |
|       **[Основные сведения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; |
|       Точное время Windows Server 2016       | 2019, 2016 | &#10004; |
|       **[Сети](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |
|       Кадры крупного размера        | 2019, 2016, 2012 R2 | &#10004; |
|       Добавление тегов и магистрали виртуальной ЛС       | 2019, 2016, 2012 R2 | &#10004;  |
|       Динамическая миграция      | 2019, 2016, 2012 R2 | &#10004; |
|       Статическая Вставка IP-адресов     |  2019, 2016, 2012 R2 | &#10004; Примечание 2 |
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; |
|       Сегментация TCP и разгрузка контрольной суммы | 2019, 2016, 2012 R2 | &#10004;|
|       SR-IOV;  | 2019, 2016 |  &#10004;   |
|       **[Память](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |
|       Изменение размера VHDX  | 2019, 2016, 2012 R2 | &#10004; |
|       Виртуальное подключение Fibre Channel | 2019, 2016, 2012 R2 | &#10004; Примечание 3  |
|       Динамическая Архивация виртуальных машин  | 2019, 2016, 2012 R2 | &#10004; Примечание 5 |
|       Поддержка TRIM | 2019, 2016, 2012 R2 | &#10004;  |
|       WWN ДЛЯ SCSI | 2019, 2016, 2012 R2 | &#10004;  |
|       **[Свободной](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |
|       Поддержка ядра PAE  | 2019, 2016, 2012 R2 |  Недоступно |
|       Настройка зазора MMIO  | 2019, 2016, 2012 R2 | &#10004; |
|       Динамическая память — "горячее" Добавление | 2019, 2016, 2012 R2  | &#10004; Примечание 7, 8, 9 |
|       Всплывающие подсказки динамическая память | 2019, 2016, 2012 R2 | &#10004; Примечание 7, 8, 9 |
|       Изменение размера памяти среды выполнения | 2019, 2016  | &#10004;  |
|       **[Роли](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | |
|       Устройство видеозаписи, определенное Hyper-V | 2019, 2016, 2012 R2 | &#10004;   |
|       **[Прочее](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | |
|       Пара "ключ-значение"  | 2019, 2016, 2012 R2 | &#10004;   |
|       Немаскируемое прерывание | 2019, 2016, 2012 R2 | &#10004;  |
|       Копирование файлов с узла на гость | 2019, 2016, 2012 R2 | &#10004;  |
|       Команда лсвмбус | 2019, 2016, 2012 R2 | &#10004;  |
|       Сокеты Hyper-V | 2019, 2016 | &#10004;  |
|       Транзитный/ДДА PCI | 2019, 2016 | &#10004; |
| **[Виртуальные машины 2-го поколения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       Загрузка с помощью UEFI | 2019, 2016, 2012 R2 |  &#10004; Примечание 12  |
|       Безопасная загрузка | 2019, 2016 |  &#10004; |

## <a name="oracle-linux-7x-series"></a>Серия Oracle Linux 7. x

В этой серии есть только 64-разрядные ядра.

<table width="100%">
<tr height="50px">
<td width="20%" rowspan="2">

Функция
</td>
<td width="20%" rowspan="2">

Версия Windows Server
</td>
<td width="30%" colspan="3">

7,5 — 7,8
</td>
<td width="30%" colspan="3">

7.3 — 7.4
</td>
</tr>
<tr>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK5
</td>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK4
</td>
</tr>
<tr>
<td width="20%">

Доступность
</td>
<td width="20%">


</td>
<td width="10%">

LIS 4,3
</td>
<td width="10%">

Встроено
</td>
<td width="10%">

Встроено
</td>
<td width="10%">

LIS 4,3
</td>
<td width="10%">

Встроено
</td>
<td width="10%">

Встроено
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Основные сведения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Точное время Windows Server 2016
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

 **[Сети](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Кадры крупного размера
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">
Добавление тегов и магистрали виртуальной ЛС
</td>
<td width="20%">
2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Динамическая миграция
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Статическая Вставка IP-адресов
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Примечание 2
</td>
<td width="10%">

&#10004; Примечание 2
</td>
<td width="10%">

&#10004; Примечание 2
</td>
<td width="10%">

&#10004; Примечание 2
</td>
<td width="10%">

&#10004; Примечание 2
</td>
<td width="10%">

&#10004; Примечание 2
</td>
</tr>
<tr height="50px">
<td width="20%">

vRSS
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Сегментация TCP и разгрузка контрольной суммы
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SR-IOV;
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Память](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Изменение размера VHDX
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Виртуальное подключение Fibre Channel
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Примечание 3
</td>
<td width="10%">

&#10004; Примечание 3
</td>
<td width="10%">

&#10004; Примечание 3
</td>
<td width="10%">

&#10004; Примечание 3
</td>
<td width="10%">

&#10004; Примечание 3
</td>
<td width="10%">

&#10004; Примечание 3
</td>
</tr>
<tr height="50px">
<td width="20%">

Динамическая Архивация виртуальных машин
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Примечание 5
</td>
<td width="10%">

&#10004; Примечание 4, 5
</td>
<td width="10%">

&#10004; Примечание 5
</td>
<td width="10%">

&#10004; Примечание 5
</td>
<td width="10%">

&#10004; Примечание 4, 5
</td>
<td width="10%">

&#10004; Примечание 5
</td>
</tr>
<tr height="50px">
<td width="20%">

Поддержка TRIM
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

WWN ДЛЯ SCSI
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[Свободной](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**
</td>
<td width="20%">


</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Поддержка ядра PAE
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

Недоступно
</td>
<td width="10%">

Недоступно
</td>
<td width="10%">

Недоступно
</td>
<td width="10%">

Недоступно
</td>
<td width="10%">

Недоступно
</td>
<td width="10%">

Недоступно
</td>
</tr>
<tr height="50px">
<td width="20%">

Настройка зазора MMIO
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Динамическая память "горячее" Добавление
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Примечание 7, 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
</tr>
<tr height="50px">
<td width="20%">

динамическая память всплывающих подсказок
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Примечание 7, 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
<td width="10%">

&#10004; Примечание 8, 9
</td>
</tr>
<tr height="50px">
<td width="20%">

Изменение размера памяти среды выполнения
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[Роли](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Видео, характерное для Hyper-V
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Прочее](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Пара "ключ-значение"
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Немаскируемое прерывание
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Копирование файлов с узла на гость
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Команда лсвмбус
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Сокеты Hyper-V
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Транзитный/ДДА PCI
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Виртуальные машины 2-го поколения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Загрузка с помощью UEFI
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Примечание 12
</td>
<td width="10%">

&#10004; Примечание 12
</td>
<td width="10%">

&#10004; Примечание 12
</td>
<td width="10%">

&#10004; Примечание 12
</td>
<td width="10%">

&#10004; Примечание 12
</td>
<td width="10%">

&#10004; Примечание 12
</td>
</tr>
<tr height="50px">
<td width="20%">

Безопасная загрузка
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
</table>


## <a name="oracle-linux-6x-series"></a>Серия Oracle Linux 6. x

В этой серии есть только 64-разрядные ядра.

|       **Компонент**     |       **Версия Windows Server**      |       **6.8-6.10 (RHCK)** |       **6.8-6.10 (UEK4)**     |
|-----------------------|---------------------------------------|-------------------|-------------------|
|       **Доступность**     |   | LIS 4,3  | Встроено  |
|       **[Основные сведения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | &#10004;
|       Точное время Windows Server 2016       | 2019, 2016 | |
|       **[Сети](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |  |
|       Кадры крупного размера        | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Добавление тегов и магистрали виртуальной ЛС       | 2019, 2016, 2012 R2 | &#10004; Примечание 1 | &#10004; Примечание 1 |
|       Динамическая миграция      | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Статическая Вставка IP-адресов     |  2019, 2016, 2012 R2 | &#10004; Примечание 2 | &#10004;|
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       Сегментация TCP и разгрузка контрольной суммы | 2019, 2016, 2012 R2 | &#10004;|  &#10004; |
|       SR-IOV;  | 2019, 2016 |    |  |
|       **[Память](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |  |
|       Изменение размера VHDX  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |
|       Виртуальное подключение Fibre Channel | 2019, 2016, 2012 R2 | &#10004; Примечание 3  | &#10004; Примечание 3 |
|       Динамическая Архивация виртуальных машин  | 2019, 2016, 2012 R2 | &#10004; Примечание 5 | &#10004; Примечание 5|
|       Поддержка TRIM | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       WWN ДЛЯ SCSI | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       **[Свободной](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  |
|       Поддержка ядра PAE  | 2019, 2016, 2012 R2 |  Недоступно | Недоступно
|       Настройка зазора MMIO  | 2019, 2016, 2012 R2 | &#10004; | &#10004;  |
|       Динамическая память — "горячее" Добавление | 2019, 2016, 2012 R2  | &#10004; Примечание 6, 8, 9 | &#10004; Примечание 6, 8, 9 |
|       Всплывающие подсказки динамическая память | 2019, 2016, 2012 R2 | &#10004; Примечание 6, 8, 9 | &#10004; Примечание 6, 8, 9 |
|       Изменение размера памяти среды выполнения | 2019, 2016  |  | |
|       **[Роли](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | | |
|       Устройство видеозаписи, определенное Hyper-V | 2019, 2016, 2012 R2 | &#10004;   | &#10004; |
|       **[Прочее](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | | |
|       Пара "ключ-значение"  | 2019, 2016, 2012 R2 | &#10004; Примечание 10, 11   | &#10004; Примечание 10, 11  |
|       Немаскируемое прерывание | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Копирование файлов с узла на гость | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Команда лсвмбус | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Сокеты Hyper-V | 2019, 2016 | &#10004;  | &#10004; |
|       Транзитный/ДДА PCI | 2019, 2016 | &#10004; | &#10004; |
| **[Виртуальные машины 2-го поколения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       Загрузка с помощью UEFI | 2019, 2016, 2012 R2 |  &#10004; Примечание 12  | &#10004; Примечание 12
|       Безопасная загрузка | 2019, 2016 |  |  |



## <a name="notes"></a><a name="BKMK_notes"></a>Примечания

1. В этом Oracle Linuxном выпуске маркировка VLAN работает, но для магистрали VLAN это не так.

2. Встраивание статических IP-адресов может не работать, если диспетчер сети настроен для конкретного искусственного сетевого адаптера на виртуальной машине. Для плавной работы внедрения статических IP-адресов убедитесь, что либо Диспетчер сети полностью выключен, либо он отключен для определенного сетевого адаптера через его файл ifcfg-ЕСКС.

3.  В Windows Server 2012 R2 при использовании виртуальных устройств Fibre Channel убедитесь, что номер логического устройства 0 (LUN 0) заполнен. Если LUN 0 не заполнен, виртуальная машина Linux может не иметь возможности подключать устройства Fibre Channel изначально.

4. Для встроенных в LIS пакетов для этой функции необходимо установить пакет Hyperv-демонов.

5.  Если во время динамической операции резервного копирования виртуальных машин имеются открытые дескрипторы файлов, то в некоторых уголках резервных виртуальных жестких дисков может потребоваться проверка согласованности файловой системы (fsck) при восстановлении. Операции динамической архивации могут автоматически завершаться сбоем, если виртуальная машина имеет подключенное устройство iSCSI или прямое подключенное хранилище (также называемое транзитным диском).

6. Поддержка динамической памяти доступна только на 64-разрядных виртуальных машинах.

7. Поддержка горячего добавления не включена по умолчанию в этом распространении. Чтобы включить поддержку "горячего" добавления, необходимо добавить правило udev в разделе/ЕТК/удев/рулес.д/следующим образом:

   1. Создайте файл **/etc/udev/Rules.d/100-Balloon.rules**. Для файла можно использовать любое другое требуемое имя.

   2. Добавьте в файл следующее содержимое: `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Перезагрузите систему, чтобы включить поддержку горячего добавления.

   Хотя Integration Services загрузки Linux создает это правило при установке, оно также удаляется при удалении LIS, поэтому правило необходимо создать заново, если после удаления потребуется динамическая память.

8. Операция динамической памяти может завершиться ошибкой, если в операционной системе на виртуальной машине слишком мало памяти. Ниже приведены некоторые рекомендации.

   * Объем памяти при запуске и минимальный объем памяти должны быть больше или равны объему памяти, рекомендуемому для поставщика распространения.

   * Приложения, которые обычно потребляют всю доступную память в системе, могут потреблять до 80 процентов доступной памяти.

9. При использовании динамическая память в операционной системе Windows Server 2016 или Windows Server 2012 R2 укажите **объем памяти при запуске**, **Минимальный объем памяти**и параметры **максимального объема памяти** (кратные 128 МБ). Несоблюдение этого действия может привести к сбоям "горячего" добавления, и в гостевой операционной системе может не появиться никакого увеличения объема памяти.

10. Чтобы включить инфраструктуру пар "ключ — значение" (KVP), установите пакет хипервквпд или программная программа Hyperv-демонов из Oracle Linux ISO. Кроме того, пакет можно установить непосредственно из Oracle Linux репозитории Yum.

11. Инфраструктура пар "ключ — значение" (KVP) может работать неправильно без обновления программного обеспечения Linux. Обратитесь к поставщику распространения, чтобы получить обновление программного обеспечения на случай возникновения проблем с этой функцией.

12. На виртуальных машинах Windows Server 2012 R2 поколения 2 по умолчанию включена безопасная загрузка, и некоторые виртуальные машины Linux не будут загружаться, если только не будет отключен параметр безопасной загрузки. Вы можете отключить безопасную загрузку в разделе **встроенное по** в параметрах виртуальной машины в **диспетчере Hyper-V** или отключить ее с помощью PowerShell:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Загрузка Integration Services Linux может быть применена к существующим виртуальным машинам поколения 2, но не внушить поколения 2.


См. также

* [Set-Вмфирмваре](/powershell/module/hyper-v/set-vmfirmware?view=win10-ps)

* [Поддерживаемые CentOS и Red Hat Enterprise Linux виртуальные машины в Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Debian в Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины SUSE в Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Ubuntu в Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины FreeBSD в Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Описания функций для виртуальных машин Linux и FreeBSD в Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Рекомендации по запуску Linux в Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)