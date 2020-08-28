---
title: восстановить
description: Справочная статья по команде revert, которая восстанавливает том обратно до указанной теневой копии.
ms.topic: reference
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc80890604b5ad1a308d1cd4df9cd23465c970d2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027282"
---
# <a name="revert"></a>восстановить

Возврат тома к указанной теневой копии. Это поддерживается только для теневых копий в контексте КЛИЕНТАКЦЕССИБЛЕ. Эти теневые копии являются постоянными и могут быть сделаны только поставщиком системы. Если используется без параметров, команда **отменить** отображение справки в командной строке.

## <a name="syntax"></a>Синтаксис

```
revert <shadowcopyID>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<shadowcopyID>` | Указывает идентификатор теневой копии для восстановления тома. Если этот параметр не используется, команда выводит справку из командной строки. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
