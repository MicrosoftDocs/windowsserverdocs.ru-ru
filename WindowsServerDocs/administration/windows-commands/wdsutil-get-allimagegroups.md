---
title: WDSUTIL Get-аллимажеграупс
description: Справочная статья по команде WDSUTIL Get-аллимажеграупс, которая извлекает сведения обо всех группах образов на сервере и всех образах в этих группах образов.
ms.topic: reference
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7209b0f806b0fd86167e8fbcf36f717a0d069195
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614866"
---
# <a name="wdsutil-get-allimagegroups"></a>WDSUTIL Get-аллимажеграупс

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения обо всех группах образов на сервере и всех образах в этих группах образов.

## <a name="syntax"></a>Синтаксис

```
wdsutil [options] /get-allimagegroups [/server:<servername>] [/detailed]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[/server:<servername>]` | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| [/детаилед] | Возвращает метаданные изображения из каждого изображения. Если этот параметр не используется, поведение по умолчанию — возврат только имени, описания и имени файла для каждого образа. |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения о группах образов, введите:

```
wdsutil /get-allimagegroups
```

```
wdsutil /verbose /get-allimagegroups /server:MyWDSServer /detailed
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Add-имажеграуп](wdsutil-add-imagegroup.md)

- [Команда WDSUTIL Remove-имажеграуп](wdsutil-remove-imagegroup.md)

- [Команда WDSUTIL Set-имажеграуп](wdsutil-set-imagegroup.md)
