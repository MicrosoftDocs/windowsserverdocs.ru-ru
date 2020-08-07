---
title: bitsadmin takeownership
description: Справочная статья по команде битсадмин такеовнершип, которая позволяет пользователю с правами администратора становиться владельцем указанного задания.
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7e37b4508681af58ab07458507101647a0906ff
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880981"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

Позволяет пользователю с правами администратора становиться владельцем указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
