---
title: bitsadmin setvalidationstate
description: Справочная статья по команде битсадмин сетвалидатионстате, которая задает состояние проверки содержимого указанного файла в задании.
ms.topic: reference
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 401412bfebb68ebb1cf0133b08ba92e9981f2a2b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820678"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

Задает состояние проверки содержимого заданного файла в задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setvalidationstate <job> <file_index> <TRUE|FALSE>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ---------- |
| Задание | Отображаемое имя задания или идентификатор GUID. |
| file_index | Начинается с 0. |
| TRUE или FALSE | **Значение true** включает проверку содержимого для указанного файла, а **значение false** отключает его. |

## <a name="examples"></a>Примеры

Чтобы установить состояние проверки содержимого файла 2 в значение TRUE для задания с именем *мидовнлоаджоб*:

```
bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
