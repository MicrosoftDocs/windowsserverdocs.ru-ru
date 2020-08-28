---
title: bitsadmin takeownership
description: Справочная статья по команде битсадмин такеовнершип, которая позволяет пользователю с правами администратора становиться владельцем указанного задания.
ms.topic: reference
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0df40e336ecc282e4b1a1774d7b5848f37a1a7a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033382"
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
