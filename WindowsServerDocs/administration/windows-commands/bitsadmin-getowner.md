---
title: bitsadmin getowner
description: Справочная статья по команде битсадмин, которая получает владельца указанного задания.
ms.topic: reference
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7308da9222b5d0d0a0ddcf75d9decf86ed85c4c3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821808"
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
