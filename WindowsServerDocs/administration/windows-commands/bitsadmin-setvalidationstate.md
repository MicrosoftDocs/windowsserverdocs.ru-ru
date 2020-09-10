---
title: bitsadmin setvalidationstate
description: Справочная статья по команде битсадмин сетвалидатионстате, которая задает состояние проверки содержимого указанного файла в задании.
ms.topic: reference
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1f30807e392ede7710c4d7740416d2cdb34c1378
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630618"
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
