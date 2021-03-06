---
title: bitsadmin takeownership
description: Справочная статья по команде битсадмин такеовнершип, которая позволяет пользователю с правами администратора становиться владельцем указанного задания.
ms.topic: reference
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 20fa23f7ae02f50d36349c43b50336d9c2412957
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820638"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

Позволяет пользователю с правами администратора становиться владельцем указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ---------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы стать владельцем задания с именем *мидовнлоаджоб*, сделайте следующее:

```
bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
