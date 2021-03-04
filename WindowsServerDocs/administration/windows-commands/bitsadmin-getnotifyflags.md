---
title: bitsadmin getnotifyflags
description: Справочная статья по команде битсадмин жетнотифифлагс, которая получает флаги уведомления для указанного задания.
ms.topic: reference
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d2fec6b2acf68f0c1d54885585a7f7f0126327a1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821848"
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

## <a name="remarks"></a>Комментарии

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
