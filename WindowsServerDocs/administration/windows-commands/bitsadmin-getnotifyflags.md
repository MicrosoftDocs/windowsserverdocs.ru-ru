---
title: bitsadmin getnotifyflags
description: Справочная статья по команде битсадмин жетнотифифлагс, которая получает флаги уведомления для указанного задания.
ms.topic: reference
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b7cdc2d65316bfcc856bb0fe55a9379d4fc6ba6b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631900"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

Получает флаги уведомления для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="remarks"></a>Примечания

Задание может содержать один или несколько следующих флагов уведомления:

| Flag | Описание |
| ----- | ----- |
| 0x001 | Создавать событие, когда все файлы в задании были переданы. |
| 0x002 | Создавать событие при возникновении ошибки. |
| 0x004 | Отключение уведомлений. |
| 0x008 | Создание события при изменении или переносе задания. |

## <a name="examples"></a>Примеры

Чтобы получить флаги уведомления для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
