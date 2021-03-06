---
title: WDSUTIL Get-аллмултикасттрансмиссионс
description: Справочная статья по WDSUTIL Get-аллмултикасттрансмиссионс, в которой отображаются сведения обо всех многоадресных передачах на сервере.
ms.topic: reference
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 49480846404b5160d5cde61c3f3a94daa5871c9e
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825278"
---
# <a name="wdsutil-get-allmulticasttransmissions"></a>WDSUTIL Get-аллмултикасттрансмиссионс

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения обо всех многоадресных передачах на сервере.

## <a name="syntax"></a>Синтаксис
для Windows Server 2008:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:Clients] [/ExcludedeletePending]
```
для Windows Server 2008 R2:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:{Boot | Install | All}] [/details:Clients]  [/ExcludedeletePending]
```
### <a name="parameters"></a>Параметры

| Параметр | Объяснение |
|--|--|
| [/Server: <Server name> ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер. |
| /Show | **Windows Server 2008**<p>/Show: Clients — отображает сведения о клиентских компьютерах, подключенных к многоадресным передачам.<p>**Windows Server 2008 R2**<p>Показывать: {Boot &#124; установить &#124; все} — тип возвращаемого образа.                                Функция **загрузки** возвращает только передачи загрузочных образов.                                  **Установка** возвращает только передачи образов. **ALL** возвращает оба типа изображений. |
|  |  |
| /детаилс: клиенты | Поддерживается только для Windows Server 2008 R2. При наличии клиенты, подключенные к передаче, будут отображаться. |
| [/Ексклудеделетепендинг] | Исключает из списка все деактивированные передачи. |

## <a name="examples"></a>Примеры
Чтобы просмотреть сведения обо всех передачах, введите:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Show:All` чтобы просмотреть сведения обо всех передачах, за исключением неактивированных передач, введите:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`

## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-мултикасттрансмиссион](wdsutil-get-multicasttransmission.md)
- [Команда WDSUTIL New-мултикасттрансмиссион](wdsutil-new-multicasttransmission.md)
- [Команда WDSUTIL Remove-мултикасттрансмиссион](wdsutil-remove-multicasttransmission.md)
- [Команда WDSUTIL Start-мултикасттрансмиссион](wdsutil-start-multicasttransmission.md)
