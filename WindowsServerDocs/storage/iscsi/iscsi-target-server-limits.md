---
title: Ограничения масштабируемости для сервера цели iSCSI
TOCTitle: iSCSI Target Server Scalability Limits
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 3867df04c83fe536473c227e43700a4758c1294e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935861"
---
# <a name="iscsi-target-server-scalability-limits"></a>Ограничения масштабируемости для сервера цели iSCSI

Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе приведены поддерживаемые и протестированные ограничения Microsoft iSCSI Target Server в Windows Server. В следующих таблицах показаны ограничения на Протестированные модули поддержки и, где это применимо, применяются ли ограничения.

## <a name="general-limits"></a>Общие ограничения

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Элемент</p></th>
<th><p>Ограничение поддержки</p></th>
<th><p>Применяются?</p></th>
<th><p>Комментировать</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>экземпляры цели iSCSI на сервер цели iSCSI</p></td>
<td><p>256</p></td>
<td><p>Нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>логические устройства iSCSI (них) или виртуальные диски на сервер цели iSCSI</p></td>
<td><p>512</p></td>
<td><p>Нет</p></td>
<td><p>Тестирование конфигураций: 8 них на целевой экземпляр с средним количеством более 64 целевых объектов и 256 целевых экземпляров с одним LU на целевой объект.</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI них или виртуальные диски на экземпляре цели iSCSI</p></td>
<td><p>256 (128 на Windows Server 2012)</p></td>
<td><p>да</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Сеансы, которые могут одновременно подключаться к экземпляру цели iSCSI</p></td>
<td><p>544 (512 на Windows Server 2012)</p></td>
<td><p>да</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Моментальные снимки на LU</p></td>
<td><p>512</p></td>
<td><p>да</p></td>
<td><p>Существует ограничение в 512 моментальных снимков на независимый том приложений iSCSI.</p></td>
</tr>
<tr class="even">
<td><p>Локально подключенные виртуальные диски или моментальные снимки на устройство хранения</p></td>
<td><p>32</p></td>
<td><p>Да</p></td>
<td><p>Локально подключенные виртуальные диски не&#39;t предлагают какие-либо функции, относящиеся к iSCSI, и являются устаревшими. Дополнительные сведения см. <a href="https://technet.microsoft.com/library/dn303411.aspx">в разделе функции, удаленные или устаревшие в Windows Server 2012 R2</a>.</p></td>
</tr>
</tbody>
</table>

## <a name="fault-tolerance-limits"></a>Ограничения отказоустойчивости

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Элемент</p></th>
<th><p>Ограничение поддержки</p></th>
<th><p>Применяются?</p></th>
<th><p>Комментировать</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Узлы отказоустойчивого кластера</p></td>
<td><p>8 (5 на Windows Server 2012)</p></td>
<td><p>Нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Несколько активных узлов кластера</p></td>
<td><p>Поддерживается</p></td>
<td>
<p>Н/Д</p></td>
<td><p>Каждый активный узел в отказоустойчивом кластере владеет другим кластеризованным экземпляром сервера цели iSCSI с другими узлами, работающими как возможные узлы-владельцы.</p></td>
</tr>
<tr class="odd">
<td><p>Уровень восстановления при ошибке (Эрл)</p></td>
<td><p>0</p></td>
<td><p>Да</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Подключений на сеанс</p></td>
<td><p>1</p></td>
<td><p>Да</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Сеансы, которые могут одновременно подключаться к экземпляру цели iSCSI</p></td>
<td><p>544 (512 на Windows Server 2012)</p></td>
<td><p>Нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Многопутевой ввод-вывод (MPIO)</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Пути MPIO</p></td>
<td><p>4</p></td>
<td><p>нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Преобразование автономного целевого сервера iSCSI в кластеризованный целевой сервер iSCSI или наоборот</p></td>
<td><p>Не поддерживается</p></td>
<td><p>Нет</p></td>
<td><p>Данные конфигурации экземпляра iSCSI и виртуального диска, включая метаданные моментального снимка, теряются во время преобразования.</p></td>
</tr>
</tbody>
</table>

## <a name="network-limits"></a>Ограничения сети

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Элемент</p></th>
<th><p>Ограничение поддержки</p></th>
<th><p>Применяются?</p></th>
<th><p>Комментировать</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Максимальное число активных сетевых адаптеров</p></td>
<td><p>8</p></td>
<td><p>Нет</p></td>
<td><p>Применяется к сетевым адаптерам, выделенным для трафика iSCSI, а не к общему числу сетевых адаптеров в устройстве.</p></td>
</tr>
<tr class="even">
<td><p>Портал (IP-адреса) поддерживается</p></td>
<td><p>64</p></td>
<td><p>Да</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Скорость сетевого порта</p></td>
<td><p>1Gbps, 10 Гбит/с, 40Gbps, 56 Гбит/с (только для Windows Server 2012 R2 и более поздние версии)</p></td>
<td><p>Нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Разгрузка TCP</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td><p>Использование большой отправки (сегментации), контрольной суммы, контроля прерываний и разгрузки RSS</p></td>
</tr>
<tr class="odd">
<td><p>разгрузка iSCSI</p></td>
<td><p>Не поддерживается</p></td>
<td><br/><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Кадры крупного размера</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPsec;</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Разгрузка CRC</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="iscsi-virtual-disk-limits"></a>ограничения виртуального диска iSCSI

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Элемент</p></th>
<th><p>Ограничение поддержки</p></th>
<th><p>Применяются?</p></th>
<th><p>Комментировать</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>От инициатора iSCSI, который преобразует виртуальный диск из базового диска в динамический </p></td>
<td><p>да</p></td>
<td><p>Нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Формат виртуального жесткого диска.</p></td>
<td><p>VHDX (только для Windows Server 2012 R2 и более поздних версий)</p>
<p>.vhd</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Минимальный размер формата виртуального жесткого диска</p></td>
<td><p>VHDX: 3 МБ</p>
<p>. VHD: 8 МБ</p></td>
<td><p>да</p></td>
<td><p>Применяется ко всем поддерживаемым типам виртуальных жестких дисков: родительский, разностный и фиксированный.</p></td>
</tr>
<tr class="even">
<td><p>Максимальный размер родительского VHD</p></td>
<td><p>VHDX: 64 ТБ</p>
<p>. VHD: 2 ТБ</p></td>
<td><p>да</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Фиксированный максимальный размер VHD</p></td>
<td><p>VHDX: 64 ТБ</p>
<p>. VHD: 16 ТБ</p></td>
<td><p>да</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Максимальный размер разностного виртуального жесткого диска</p></td>
<td><p>VHDX: 64 ТБ</p>
<p>. VHD: 2 ТБ</p></td>
<td><p>да</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Фиксированный формат VHD</p></td>
<td><p>Поддерживается</p></td>
<td><p>Нет</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Разностный формат VHD</p></td>
<td><p>Поддерживается</p></td>
<td><p>Нет</p></td>
<td><p>Моментальные снимки не могут быть созданы с разностными виртуальными дисками iSCSI на основе VHD.</p></td>
</tr>
<tr class="odd">
<td><p>Количество разностных виртуальных жестких дисков на родительский виртуальный жесткий диск</p></td>
<td><p>256</p></td>
<td><p>Нет (да в Windows Server 2012)</p></td>
<td><p>Два уровня глубины (файлы внуками. VHDX) — максимум для VHDX-файлов; один уровень глубины (дочерние VHD-файлы) является максимальным для VHD-файлов.</p></td>
</tr>
<tr class="even">
<td><p>Динамический формат VHD</p></td>
<td><p>VHDX: Да</p>
<p>. VHD: Да (нет в Windows Server 2012)</p></td>
<td><p>да</p></td>
<td><p>Несопоставление не поддерживается&#39;t.</p></td>
</tr>
<tr class="odd">
<td><p>exFAT/FAT32/FAT (объем размещения виртуального жесткого диска)</p></td>
<td><p>Не поддерживается</p></td>
<td><p>Да</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CSV v2</p></td>
<td><p>Не поддерживается</p></td>
<td><p>Да</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ReFS</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>NTFS</p></td>
<td><p>Поддерживается</p></td>
<td><p>Н/Д</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>CFS не Майкрософт</p></td>
<td><p>Не поддерживается</p></td>
<td><p>Да</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Тонкая подготовка</p></td>
<td><p>Нет</p></td>
<td><p>Недоступно</p></td>
<td><p>Динамические виртуальные жесткие диски поддерживаются, но сопоставление не поддерживается&#39;t.</p></td>
</tr>
<tr class="odd">
<td><p>Сжатие логического устройства</p></td>
<td><p>Да (только для Windows Server 2012 R2 и более поздних версий)</p></td>
<td><p>Н/Д</p></td>
<td><p>Чтобы сжать LUN, используйте <a href="https://docs.microsoft.com/powershell/module/iscsitarget/resize-iscsivirtualdisk">resize-исксивиртуалдиск</a> .</p></td>
</tr>
<tr class="even">
<td><p>Клонирование логических устройств</p></td>
<td><p>Не поддерживается</p></td>
<td><p>Н/Д</p></td>
<td><p>Вы можете быстро клонировать данные диска с помощью разностных виртуальных жестких дисков.</p></td>
</tr>
</tbody>
</table>

## <a name="snapshot-limits"></a>Ограничения по числу моментальных снимков

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Элемент</p></th>
<th><p>Ограничение поддержки</p></th>
<th><p>Комментировать</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Создание моментального снимка</p></td>
<td><p>Поддерживается</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Восстановление моментального снимка</p></td>
<td><p>Поддерживается</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Моментальные снимки с возможностью записи</p></td>
<td><p>Не поддерживается</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Моментальный снимок — преобразование в полное</p></td>
<td><p>Не поддерживается</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Моментальный снимок — откат в сети</p></td>
<td><p>Не поддерживается</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Моментальный снимок — преобразовать в записываемый</p></td>
<td><p>Не поддерживается</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Перенаправление моментального снимка</p></td>
<td><p>Не поддерживается</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Закрепление моментальных снимков</p></td>
<td><p>Не поддерживается</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Локальное подключение</p></td>
<td><p>Поддерживается</p></td>
<td><p>Локально подключенные виртуальные диски iSCSI являются устаревшими. Дополнительные сведения см. <a href="https://technet.microsoft.com/library/dn303411.aspx">в разделе функции, удаленные или устаревшие в Windows Server 2012 R2</a>. Динамические моментальные снимки диска не могут быть подключены локально.</p></td>
</tr>
</tbody>
</table>

## <a name="iscsi-target-server-manageability-and-backup"></a>управляемость и резервное копирование сервера цели iSCSI

Если вы хотите создать теневые копии томов (моментальные снимки открытых файлов VSS) для данных на виртуальных дисках iSCSI с сервера приложений, или вы хотите управлять виртуальными дисками iSCSI с помощью более старого приложения (например, команды DiskRAID), для которого требуется поставщик оборудования службы виртуальных дисков (VDS), установите поставщик хранилища цели iSCSI на сервере, с которого требуется создать моментальный снимок, или используйте приложение управления VDS.

Поставщик хранилища цели iSCSI — это служба роли в Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012; Кроме того, вы можете скачать и установить [поставщики хранилища цели iSCSI (VDS/VSS) для серверов приложений нижнего уровня](https://www.microsoft.com/download/details.aspx?id=34759) в следующих операционных системах, если сервер цели iSCSI работает под управлением Windows Server 2012:

  - Windows Storage Server 2008 R2

  - Windows Server 2008 R2

  - Windows HPC Server 2008 R2

  - Windows HPC Server 2008

Обратите внимание, что если сервер цели iSCSI размещен на сервере под управлением Windows Server 2012 R2 или более поздней версии и вы хотите использовать VSS или VDS с удаленного сервера, на удаленном сервере также должна быть установлена та же версия Windows Server и служба роли поставщика хранилища цели iSCSI. Также обратите внимание, что во всех версиях Windows необходимо установить только одну версию службы роли поставщика хранилища цели iSCSI.

Дополнительные сведения о поставщике хранилища цели iSCSI см. в статье [поставщик целевого хранилища iSCSI (VDS/VSS)](/powershell/module/iscsi/?view=win10-ps).

## <a name="tested-compatibility-with-iscsi-initiators"></a>Протестированы совместимость с инициаторами iSCSI

Мы протестировали программное обеспечение iSCSI Target Server с помощью следующих инициаторов iSCSI:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Инициатор</p></td>
<td><p>Windows Server 2012 R2</p></td>
<td><p>Windows Server 2012</p></td>
<td><p>Комментарии</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>Проверено</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003</p></td>
<td><p>Проверено</p></td>
<td><p>Проверено</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare vSphere 5</p></td>
<td></td>
<td><p>Проверено</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VMWare ESXi 5,0</p></td>
<td><p>Проверено</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare ESX 4,1</p></td>
<td><p>Проверено</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>CentOS 6.x</p></td>
<td><p>Проверено</p></td>
<td></td>
<td><p>Необходимо выйти из сеанса и снова войти в систему для обнаружения измененного размера виртуального диска.</p></td>
</tr>
<tr class="even">
<td><p>Red Hat Enterprise Linux 6</p></td>
<td><p>Проверено</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>RedHat Enterprise Linux 5 и 5</p></td>
<td><p>Проверено</p></td>
<td><p>Проверено</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>SUSE Linux Enterprise Server 10</p></td>
<td></td>
<td><p>Проверено</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Oracle Solaris 11. x</p></td>
<td><p>Проверено</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

Мы также проверили следующие инициаторы iSCSI, выполняющие бездисковую загрузку с виртуальных дисков, размещенных на сервере iSCSI Target Server:

  - Windows Server 2012 R2

  - Windows Server 2012

  - Сетевой адаптер PCIe с Ипксе

  - CD или USB-диск с Ипксе

## <a name="additional-references"></a>Дополнительные ссылки

Ниже перечислены дополнительные ресурсы с информацией о сервере цели iSCSI и связанных технологиях.

- [Обзор блочного хранилища цели iSCSI](iscsi-target-server.md)

- [Обзор загрузки цели iSCSI](iscsi-boot-overview.md)

- [Хранилище в Windows Server](../storage.yml)
