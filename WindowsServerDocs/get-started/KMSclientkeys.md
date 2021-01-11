---
title: Ключи установки клиента KMS
description: Ключи, необходимые для активации продуктов Windows на сервере KMS
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 11/12/2019
ms.topic: how-to
ms.openlocfilehash: 6e39590e1581056f741585fa1123d8db9ac764cf
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949250"
---
# <a name="kms-client-setup-keys"></a>Ключи установки клиента KMS

>Применяется к: Windows Server 2019, Windows Server Semi-Annual Channel, Windows Server 2016, Windows 10

Компьютеры, работающие под управлением лицензируемых версий Windows Server, Windows 10, Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, Windows Server 2008 R2, Windows Vista, и Windows Server 2008, по умолчанию являются клиентами KMS, для которых не требуется дополнительная настройка.

> [!NOTE]
> В приведенных далее таблицах LTSC означает Long-Term Servicing Channel, а LTSB — Long-Term Servicing Branch.

**Чтобы использовать перечисленные здесь ключи (универсальные ключи многократной установки), в своей среде сначала нужно запустить узел KMS.** Если узел KMS еще не настроен, обратитесь к разделу [Deploy KMS Activation](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502531(v=ws.11)) (Развертывание активации KMS), в котором рассматривается процедура установки.

При преобразовании узла KMS, компьютера, использующего ключ MAK или работающего под управлением розничной лицензионной версии Windows, в клиент KMS необходимо установить соответствующий ключ установки (GVLK) из приведенных ниже таблиц. Чтобы установить ключ установки клиента, откройте командную строку администратора в клиенте, введите **slmgr /ipk \<setup key\>** и нажмите клавишу **ВВОД**.

| Действие    | Ресурс   |
|--------------------|------------------------|
| При активации Windows вне сценария активации корпоративных лицензий (то есть при активации розничной версии Windows) **эти ключи работать не будут**. | Для розничных версий Windows используйте следующие ссылки: |
| Исправьте ошибку, которую вы получили при попытке активации системы Windows 8.1, Windows Server 2012 R2 или более новой системы. "Error: 0xC004F050 The Software Licensing Service reported that the product key is invalid…" | [Установите это обновление](https://support.microsoft.com/help/3172614/july-2016-update-rollup-for-windows-8-1-and-windows-server-2012-r2) на узле KMS, если он работает под управлением Windows 8.1, Windows Server 2012 R2, Windows 8 или Windows Server 2012. |

-   [Получение Windows 10](https://www.microsoft.com/windows/get-windows-10)

-   [Получение нового ключа продукта Windows](https://support.microsoft.com/help/10749/windows-product-key)

-   [Подлинная система Windows. Справка и инструкции](https://support.microsoft.com/help/15087/windows-genuine)


>   Если вы используете Windows Server 2008 R2 или Windows 7, необходимо внимательно отслеживать обновления для поддержки использования этих систем в качестве узлов KMS для клиентов Windows 10.

## <a name="windows-server-semi-annual-channel-versions"></a>Версии Semi-Annual Channel для Windows Server

### <a name="windows-server-version-1909-version-1903-and-version-1809"></a>Windows Server версий 1909, 1903 и 1809

| Версия операционной системы  | Ключ установки клиента KMS          |
|---------------------------|-------------------------------|
| Windows Server Datacenter | 6NMRW-2C8FM-D24W7-TQWMY-CWH2D |
| Windows Server Standard   | N2KJX-J94YW-TQVFB-DG9YT-724CC |

## <a name="windows-server-ltscltsb-versions"></a>Версии Windows Server LTSC и LTSB

### <a name="windows-server-2019"></a>Windows Server 2019
| Версия операционной системы       | Ключ установки клиента KMS          |
|--------------------------------|-------------------------------|
| Windows Server 2019 Datacenter | WMDGN-G9PQG-XVVXX-R3X43-63DFG |
| Windows Server 2019 Standard   | N69G4-B89J2-4G8F4-WWYCC-J464C |
| Windows Server 2019 Essentials | WVDHN-86M7X-466P6-VHXV7-YY726 |

### <a name="windows-server-2016"></a>Windows Server 2016

| Версия операционной системы       | Ключ установки клиента KMS          |
|--------------------------------|-------------------------------|
| Windows Server 2016 Datacenter | CB7KF-BWN84-R7R2Y-793K2-8XDDG |
| Windows Server 2016 Standard   | WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY |
| Windows Server 2016 Essentials | JCKRF-N37P4-C2D82-9YXRT-4M63B |

## <a name="windows-10-all-supported-semi-annual-channel-versions"></a>Windows 10, все поддерживаемые версии Semi-Annual Channel

См. в разделе [Справочные материалы по жизненному циклу Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) сведения о поддерживаемых версиях и конечных датах обслуживания.

| Версия операционной системы          | Ключ установки клиента KMS          |
|-----------------------------------|-------------------------------|
| Windows 10 Pro                    | W269N-WFGWX-YVC9B-4J6C9-T83GX |
| Windows 10 Pro N                  | MH37W-N47XK-V7XM9-C7227-GCQG9 |
| Windows 10 Pro для рабочих станций   | NRG8B-VKK3Q-CXVCJ-9G2XF-6Q84J |
| Windows 10 Pro для рабочих станций N | 9FNHH-K3HBT-3W4TD-6383H-6XYWF |
| Windows 10 Pro для образовательных учреждений          | 6TP4R-GNPTD-KYYHQ-7B7DP-J447Y |
| Windows 10 Pro для образовательных учреждений N        | YVWGF-BXNMC-HTQYQ-CPQ99-66QFC |
| Windows 10 для образовательных учреждений              | NW6C2-QMPVW-D7KKK-3GKT6-VCFB2 |
| Windows 10 для образовательных учреждений N            | 2WH4N-8QGBV-H22JP-CT43Q-MDWWJ |
| Windows 10 Корпоративная             | NPPR9-FWDCX-D2C8J-H872K-2YT43 |
| Windows 10 Корпоративная N           | DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4 |
| Windows 10 Корпоративная G           | YYVX9-NTFWV-6MDM3-9PT4T-4M68B |
| Windows 10 Корпоративная G N         | 44RPN-FTY23-9VTTB-MP9BX-T84FV |

## <a name="windows-10-ltscltsb-versions"></a>Версии Windows 10 LTSC и LTSB

### <a name="windows-10-ltsc-2019"></a>Windows 10 LTSC 2019

| Версия операционной системы          | Ключ установки клиента KMS          |
|-----------------------------------|-------------------------------|
| Windows 10 Корпоративная LTSC 2019   | M7XTQ-FN8P6-TTKYV-9D4CC-J462D |
| Windows 10 Корпоративная N LTSC 2019 | 92NFX-8DJQP-P6BBQ-THF9C-7CG2H |

### <a name="windows-10-ltsb-2016"></a>Windows 10 LTSB 2016

| Версия операционной системы          | Ключ установки клиента KMS          |
|-----------------------------------|-------------------------------|
| Windows 10 Корпоративная LTSB 2016   | DCPHK-NFMTC-H88MJ-PFHPY-QJ4BJ |
| Windows 10 Корпоративная N LTSB 2016 | QFFDN-GRT3P-VKWWX-X7T3R-8B639 |

### <a name="windows-10-ltsb-2015"></a>Windows 10 LTSB 2015

| Версия операционной системы          | Ключ установки клиента KMS          |
|-----------------------------------|-------------------------------|
| Windows 10 Корпоративная 2015 с долгосрочным обслуживанием   | WNMTR-4C88C-JK8YV-HQ7T2-76DF9 |
| Windows 10 Корпоративная 2015 с долгосрочным обслуживанием N | 2F77B-TNFGY-69QQF-B8YKP-D69TJ |

## <a name="earlier-versions-of-windows-server"></a>Предшествующие версии Windows Server

### <a name="windows-server-version-1803"></a>Windows Server версии 1803

| Версия операционной системы  | Ключ установки клиента KMS          |
|---------------------------|-------------------------------|
| Windows Server Datacenter | 2HXDN-KRXHB-GPYC7-YCKFJ-7FVDG |
| Windows Server Standard   | PTXN8-JFHJM-4WC78-MPCBR-9W4KR |

### <a name="windows-server-version-1709"></a>Windows Server версии 1709

| Версия операционной системы  | Ключ установки клиента KMS          |
|---------------------------|-------------------------------|
| Windows Server Datacenter | 6Y6KB-N82V8-D8CQV-23MJW-BWTG6 |
| Windows Server Standard   | DPCNP-XQFKJ-BJF7R-FRC8D-GF6G4 |

### <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

| Версия операционной системы               | Ключ установки клиента KMS          |
|----------------------------------------|-------------------------------|
| Windows Server 2012 R2 Server Standard | D2N9P-3P6X9-2R39C-7RTCD-MDVJX |
| Windows Server 2012 R2 Datacenter      | W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9 |
| Windows Server 2012 R2 Essentials      | KNC87-3J2TX-XB4WP-VCPJV-M4FWM |

### <a name="windows-server-2012"></a>Windows Server 2012

| Версия операционной системы                | Ключ установки клиента KMS          |
|-----------------------------------------|-------------------------------|
| Windows Server 2012                     | BN3D2-R7TKB-3YPBD-8DRP2-27GG4 |
| Windows Server 2012 N                   | 8N2M2-HWPGY-7PGT9-HGDD8-GVGGY |
| Windows Server 2012 для одного языка     | 2WN2H-YGCQR-KFX6K-CD6TF-84YXQ |
| Windows Server 2012 для конкретной страны    | 4K36P-JN4VD-GDC6V-KDT89-DYFKP |
| Windows Server 2012 Server Standard     | XC9B7-NBPP2-83J2H-RHMBY-92BT4 |
| Windows Server 2012 MultiPoint Standard | HM7DN-YVMH3-46JC3-XYTG7-CYQJJ |
| Windows Server 2012 MultiPoint Premium  | XNH6W-2V9GX-RGJ4K-Y8X6F-QGJ2G |
| Windows Server 2012 Datacenter          | 48HP8-DN98B-MYWDG-T2DCC-8W83P |


### <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

| Версия операционной системы                         | Ключ установки клиента KMS          |
|--------------------------------------------------|-------------------------------|
| Windows Server 2008 R2 Web                       | 6TPJF-RBVHG-WBW2R-86QPH-6RTM4 |
| Windows Server 2008 R2 HPC Edition               | TT8MH-CG224-D3D7Q-498W2-9QCTX |
| Windows Server 2008 R2 Standard                  | YC6KT-GKW9T-YTKYR-T4X34-R7VHC |
| Windows Server 2008 R2 Enterprise                | 489J6-VHDMP-X63PK-3K798-CPX3Y |
| Windows Server 2008 R2 Datacenter                | 74YFP-3QFB3-KQT8W-PMXWJ-7M648 |
| Windows Server 2008 R2 for Itanium-based Systems | GT63C-RJFQ3-4GMB6-BRFB9-CB83V |

### <a name="windows-server-2008"></a>Windows Server 2008

| Версия операционной системы                       | Ключ установки клиента KMS          |
|------------------------------------------------|-------------------------------|
| Windows Web Server 2008                        | WYR28-R7TFJ-3X2YQ-YCY4H-M249D |
| Windows Server 2008 Standard                   | TM24T-X9RMF-VWXK6-X8JC9-BFGM2 |
| Windows Server 2008 Standard без Hyper-V   | W7VD6-7JFBR-RX26B-YKQ3Y-6FFFJ |
| Windows Server 2008 Enterprise                 | YQGMW-MPWTJ-34KDK-48M3W-X4Q6V |
| Windows Server 2008 Enterprise без Hyper-V | 39BXF-X8Q23-P2WWT-38T2F-G3FPG |
| Windows Server 2008 HPC                        | RCTX3-KWVHP-BR6TB-RB6DM-6X7HP |
| Windows Server 2008 Datacenter                 | 7M67G-PC374-GR742-YH8V4-TCBY3 |
| Windows Server 2008 Datacenter без Hyper-V | 22XQ2-VRXRG-P8D42-K34TD-G3QQC |
| Windows Server 2008 для систем на базе процессоров Itanium  | 4DWFP-JF3DJ-B7DTH-78FJB-PDRHK |

## <a name="earlier-versions-of-windows"></a>Предшествующие версии Windows

### <a name="windows-81"></a>Windows 8.1

| Версия операционной системы | Ключ установки клиента KMS          |
|--------------------------|-------------------------------|
| Windows 8.1 Профессиональная          | GCRJD-8NW9H-F2CDX-CCM8D-9D6T9 |
| Windows 8.1 Pro N        | HMCNV-VVBFX-7HMBH-CTY9B-B4FXY |
| Windows 8.1 Корпоративная   | MHF9N-XY6XB-WVXMC-BTDCT-MKKG7 |
| Windows 8.1 Корпоративная N | TT4HM-HN7YT-62K67-RGRQJ-JFFXW |

### <a name="windows-8"></a>Windows 8

| Версия операционной системы | Ключ установки клиента KMS          |
|--------------------------|-------------------------------|
| Windows 8 Профессиональная            | NG4HW-VH26C-733KW-K6F98-J8CK4 |
| Windows 8 Pro N          | XCVCF-2NXM9-723PB-MHCB7-2RYQQ |
| Windows 8 Корпоративная     | 32JNW-9KQ84-P47T8-D8GGY-CWCK7 |
| Windows 8 Корпоративная N   | JMNMF-RHW7P-DMY6X-RF3DR-X2BQT |


### <a name="windows-7"></a>Windows 7

| Версия операционной системы | Ключ установки клиента KMS          |
|--------------------------|-------------------------------|
| Windows 7 Профессиональная   | FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4 |
| Windows 7 Профессиональная N | MRPKT-YTG23-K7D7T-X2JMM-QY7MG |
| Windows 7 Профессиональная E | W82YF-2Q76Y-63HXB-FGJG9-GF7QX |
| Windows 7 Корпоративная     | 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH |
| Windows 7 Корпоративная N   | YDRBP-3D83W-TY26F-D46B2-XCKRJ |
| Windows 7 Корпоративная E   | C29WB-22CC8-VJ326-GHFJW-H9DH4 |


См. также статью

• [Планирование активации корпоративных лицензий](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134042(v=ws.11))
