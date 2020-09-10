---
title: bitsadmin getowner
description: Справочная статья по команде битсадмин, которая получает владельца указанного задания.
ms.topic: reference
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2839936113e304e9c57308042f5c8cf66e887d36
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631874"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

Отображает отображаемое имя или идентификатор GUID владельца указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы отобразить владельца для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
