---
title: WDSUTIL Get-аллимажес
description: Справочная статья по команде WDSUTIL Get-аллимажес, которая получает сведения обо всех изображениях на сервере.
ms.topic: reference
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 632d16be639394f5e251eaa2ec98b388f200b13d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825901"
---
# <a name="wdsutil-get-allimages"></a>WDSUTIL Get-аллимажес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения обо всех образах на сервере.

## <a name="syntax"></a>Синтаксис

```
wdsutil /get-allimages [/server:<servername>] /show:{boot | install | legacyris | all} [/detailed]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[/server:<servername>]` | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| `/show:{boot | install | legacyris | all}` | Если при **загрузке** возвращаются только загрузочные образы, **Установка** возвращает образы установки, а также сведения о группах образов, содержащих их, **легацирис** возвращает только образы служб удаленной установки (RIS), а **все** данные — образ загрузки, сведения об установке образа (включая сведения о группах образов) и сведения об образе RIS. |
| [/детаилед] | Указывает, что должны возвращаться все метаданные изображения из каждого изображения. Если этот параметр не используется, поведение по умолчанию — возврат только имени, описания и имени файла изображения. |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения об образах, введите:

```
wdsutil /get-allimages /show:install
```

```
wdsutil /verbose /get-allimages /server:MyWDSServer /show:all /detailed
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-Image](wdsutil-add-image.md)

- [Команда WDSUTIL Copy-Image](wdsutil-copy-image.md)

- [Команда WDSUTIL Export-Image](wdsutil-export-image.md)

- [Команда WDSUTIL Remove-Image](wdsutil-remove-image.md)

- [Команда WDSUTIL Replace-Image](wdsutil-replace-image.md)

- [Команда WDSUTIL Set-Image](wdsutil-set-image.md)
