---
title: create volume simple
description: Справочная статья по команде CREATE VOLUME Simple, которая создает простой том на указанном динамическом диске.
ms.topic: reference
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5795f7d4ff8c14d93b90ff4a240f42793c753bb3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819308"
---
# <a name="create-volume-simple"></a>create volume simple

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает простой том на указанном динамическом диске. После создания тома фокус автоматически переместится на новый том.

## <a name="syntax"></a>Синтаксис

```
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Размер =`<n>`  | Размер тома в мегабайтах (МБ). Если размер не указан, новый том занимает оставшееся свободное пространство на диске. |
| диск =`<n>`  | Динамический диск, на котором создается том. Если диск не указан, используется текущий диск. |
| Выровняйте =`<n>` | Выравнивает все экстенты томов по ближайшей границе выравнивания. Обычно используется с массивами LUN аппаратного RAID-массива для повышения производительности. `<n>` количество килобайтов (КБ) от начала диска до ближайшей границы выравнивания. |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="examples"></a>Примеры

Чтобы создать том размером 1000 МБ, на диске 1 введите:

```
create volume simple size=1000 disk=1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [создать команду](create.md)
