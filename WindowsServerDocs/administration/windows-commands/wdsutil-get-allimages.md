---
title: WDSUTIL Get-аллимажес
description: Справочная статья по WDSUTIL Get-аллимажес, которая извлекает сведения обо всех образах на сервере.
ms.topic: reference
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fc4234e199d0eb39c3f8d94c31f2330f60cdc167
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730884"
---
# <a name="wdsutil-get-allimages"></a>WDSUTIL Get-аллимажес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения обо всех образах на сервере.

## <a name="syntax"></a>Синтаксис
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Show: {Загрузка &#124; установка &#124; Легацирис &#124; все}|-   **Boot** возвращает только загрузочные образы.<br />-   **Install** возвращает образы установки, а также сведения о группах образов, содержащих их.<br />-   **Легацирис** возвращает только образы служб удаленной установки (RIS).<br />-   **Все** возвращает сведения об образе загрузки, сведения об образе установки (включая сведения о группах образов) и сведения об образе RIS.|
|[/детаилед]|Указывает, что должны возвращаться все метаданные изображения из каждого изображения. Если этот параметр не используется, поведение по умолчанию — возврат только имени, описания и имени файла изображения.|
## <a name="examples"></a>Примеры
Чтобы просмотреть сведения об образах, введите одно из следующих действий:
```
wdsutil /Get-AllImages /Show:Install
wdsutil /verbose /Get-AllImages /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-Image](wdsutil-add-image.md)
- [Команда WDSUTIL Copy-Image](wdsutil-copy-image.md)
- [Команда WDSUTIL Export-Image](wdsutil-export-image.md)
- [Команда WDSUTIL Remove-Image](wdsutil-remove-image.md)
- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)
- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)