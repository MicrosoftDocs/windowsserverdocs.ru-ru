---
title: Get-Аллимажес
description: Справочная статья по Get-Аллимажес, которая извлекает сведения обо всех изображениях на сервере.
ms.topic: reference
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 79b28d3649e18b192504bf6eb012984cb43218e2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626384"
---
# <a name="get-allimages"></a>Get-Аллимажес

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
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-add-image-command.md) 
 Add-Image [Использование команды](using-the-copy-image-command.md) 
 Copy-Image [Использование команды](using-the-export-image-command.md) 
 Export-Image [Использование команды](using-the-remove-image-command.md) 
 Remove-Image [Использование команды](using-the-replace-image-command.md) 
 Replace-Image [Подкоманда: Set-Image](subcommand-set-image.md)
