---
title: load metadata
description: Справочная статья по команде Load metadata, которая загружает файл metadata. cab перед импортом транспортной теневой копии или загружает метаданные модуля записи в случае восстановления.
ms.topic: reference
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0acb8fc0b564b16c0a69c6d5176ef229a7e6edd7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814110"
---
# <a name="load-metadata"></a>Загрузить метаданные

Загружает файл metadata. cab перед импортом транспортной теневой копии или загружает метаданные модуля записи в случае восстановления. Если используется без параметров, при **загрузке метаданных** в командной строке отображается справка.

## <a name="syntax"></a>Синтаксис

```
load metadata [<drive>:][<path>]<metadata.cab>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `[<drive>:][<path>]` | Указывает расположение файла метаданных. |
| metadata.cab | Указывает файл metadata. cab для загрузки. |

## <a name="remarks"></a>Комментарии

- С помощью команды **Import** можно импортировать транспортную теневую копию на основе метаданных, указанных в параметре **загрузить метаданные**.

- Эту команду необходимо выполнить перед командой **Begin Restore** , чтобы загрузить выбранные модули записи и компоненты для восстановления.

## <a name="examples"></a>Примеры

Чтобы загрузить файл метаданных с именем metafile.cab из расположения по умолчанию, введите:

```
load metadata metafile.cab
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Import DiskShadow](import.md)

- [Команда Begin Restore](begin-restore.md)
