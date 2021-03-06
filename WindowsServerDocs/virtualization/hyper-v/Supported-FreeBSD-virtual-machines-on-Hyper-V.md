---
title: Поддерживаемые виртуальные машины FreeBSD в Hyper-V
description: Список служб и компонентов интеграции FreeBSD/Linux, входящих в каждую версию
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
ms.author: benarm
author: BenjaminArmstrong
ms.date: 01/08/2021
ms.openlocfilehash: cfda833dd6c644eec85b3f4914c89449bb906880
ms.sourcegitcommit: 209b0995a11c89bb9ece3db0d48a35d7ba5bbd9d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2021
ms.locfileid: "98053587"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>Поддерживаемые виртуальные машины FreeBSD в Hyper-V

>Применимо к: Azure Stack ХЦИ, версия 20H2; Windows Server 2019, Hyper-V Server 2019, Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows 10, Windows 8.1

Следующая схема распределения признаков показывает функции в каждой версии. Известные проблемы и способы их решения для каждого распространения перечислены после таблицы.

## <a name="table-legend"></a>Условные обозначения таблицы

* В состав этого выпуска FreeBSD входит **Встроенная** служба интеграции FreeBSD.

* &#10004;-доступный компонент

* (*пусто*) — функция недоступна

|**Возможность**|**Версия операционной системы Windows Server**|**12-12,1**|**11.1 — 11.3**|**11,0**|**10.3**|**10.2**|**10,0-10,1**|**9,1-9,3, 8,4**|
|-|-|-|-|-|-|-|-|-|
|**Доступность**||Встроено|Встроено|Встроено|Встроено|Встроено|Встроено|[Порты](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Основные сведения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Точное время Windows Server 2016|2019, 2016|&#10004;|&#10004;||||||
|**[Сеть](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Кадры крупного размера|2019, 2016, 2012 R2|&#10004; Примечание 3|&#10004; Примечание 3|&#10004; Примечание 3|&#10004; Примечание 3|&#10004; Примечание 3|&#10004; Примечание 3|&#10004; Примечание 3|
|Добавление тегов и магистрали виртуальной ЛС|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Динамическая миграция|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Статическая Вставка IP-адресов|2019, 2016, 2012 R2|&#10004; Примечание 4|&#10004; Примечание 4|&#10004; Примечание 4|&#10004; Примечание 4|&#10004; Примечание 4|&#10004; Примечание 4|&#10004;|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|||||
|Сегментация TCP и разгрузка контрольной суммы|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|||
|Разгрузка крупного приема (ЛРО)|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||||
|SR-IOV;|2019, 2016|&#10004;|&#10004;|&#10004;|||||
|**[Память](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||NOTE1|Примечание 1|Примечание 1|Примечание 1|Примечание 1|Примечание 1, 2|Примечание 1, 2|
|Изменение размера VHDX|2019, 2016, 2012 R2|&#10004; Примечание 6|&#10004; Примечание 6|&#10004; Примечание 6|||||
|Виртуальное подключение Fibre Channel|2019, 2016, 2012 R2||||||||
|Динамическая Архивация виртуальных машин|2019, 2016, 2012 R2|&#10004;|&#10004;||||||
|Поддержка TRIM|2019, 2016, 2012 R2|&#10004;|&#10004;||||||
|WWN ДЛЯ SCSI|2019, 2016, 2012 R2||||||||
|**[Свободной](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|||||||||
|Поддержка ядра PAE|2019, 2016, 2012 R2||||||||
|Настройка зазора MMIO|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Динамическая память Hot-Add|2019, 2016, 2012 R2||||||||
|Всплывающие подсказки динамическая память|2019, 2016, 2012 R2||||||||
|Изменение размера памяти среды выполнения|2019, 2016||||||||
|**[Роли](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**|||||||||
|Устройство, относящееся к Hyper-V|2019, 2016, 2012 R2||||||||
|**[Прочее](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**|||||||||
|Пара "ключ — значение"|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; Примечание 5|&#10004;|
|Немаскируемое прерывание|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Копирование файлов с узла на гость|2019, 2016, 2012 R2||||||||
|Команда лсвмбус|2019, 2016, 2012 R2||||||||
|Сокеты Hyper-V|2019, 2016||||||||
|Транзитный/ДДА PCI|2019, 2016|&#10004;|&#10004;||||||
|**[Виртуальные машины 2-го поколения](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|||||||||
|Загрузка с помощью UEFI|2019, 2016, 2012 R2|&#10004;|&#10004;||||||
|Безопасная загрузка|2019, 2016||||||||

## <a name="notes"></a><a name="BKMK_notes"></a>Примечания

1. Предложите, чтобы [пометить дисковые устройства]( https://www.freebsd.org/doc/handbook/geom-glabel.html) , чтобы избежать ошибок корневого подключения во время запуска.

2. Виртуальный DVD-дисковод может не располагаться при загрузке драйверов BIS в FreeBSD 8. x и 9. x, если не включить устаревший драйвер ATA с помощью следующей команды.
    ```sh
    # echo ‘hw.ata.disk_enable=1' >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126 — максимальный поддерживаемый размер MTU.

4. В сценарии отработки отказа нельзя задать статический IPv6-адрес на сервере реплики. Вместо этого используйте IPv4-адрес.

5. KVP предоставляется портами в FreeBSD 10,0. Дополнительные сведения см. в статье [порты FreeBSD 10,0](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) на FreeBSD.org.

6. Чтобы изменить размер VHDX-файла в сети в FreeBSD 11,0, необходимо выполнить Специальный шаг вручную, чтобы обойти ошибку ЖЕОМ, которая исправлена в 11.0 +, после того, как узел изменится на диск VHDX, откроет диск для записи, а затем выполните команду "гпарт resizing", как показано ниже.
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```

**Дополнительные примечания**. Матрица возможностей 10 стабильных и 11 стабильных компонентов аналогична выпуску FreeBSD 11,1. Кроме того, FreeBSD 10,2 и предыдущие версии (10,1, 10,0, 9. x, 8. x) в конце жизни. Ознакомьтесь со списком поддерживаемых выпусков и новейшими рекомендациями [по безопасности](https://security.freebsd.org/) .

## <a name="see-also"></a>См. также:

* [Описания функций для виртуальных машин Linux и FreeBSD в Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Рекомендации по запуску FreeBSD в Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
