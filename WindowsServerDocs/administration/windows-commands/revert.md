---
title: восстановить
description: Справочная статья по команде revert, которая восстанавливает том обратно до указанной теневой копии.
ms.topic: reference
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 693aa3bb91043c56a14435e7d96881b833b5f648
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806837"
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
