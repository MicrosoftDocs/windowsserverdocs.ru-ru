---
title: WDSUTIL Get-аллимажеграупс
description: Справочная статья по команде WDSUTIL Get-аллимажеграупс, которая извлекает сведения обо всех группах образов на сервере и всех образах в этих группах образов.
ms.topic: reference
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 579c71738d2f7b82cdc2e4623053569590106770
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825268"
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
