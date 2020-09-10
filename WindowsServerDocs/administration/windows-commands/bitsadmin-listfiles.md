---
title: bitsadmin listfiles
description: Справочная статья по команде битсадмин листфилес, в которой перечислены файлы в указанном задании.
ms.topic: reference
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 702c2d3d3370275373a91aef63aa82f7e84bcf14
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631510"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Перечисляет файлы в указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить список файлов для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
