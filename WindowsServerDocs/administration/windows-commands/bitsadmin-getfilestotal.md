---
title: bitsadmin getfilestotal
description: Справочная статья по команде битсадмин жетфилестотал, которая получает количество файлов в указанном задании.
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09867e5ed8b060f7a9cbfe573c6e98bfbac831df
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894333"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

Извлекает количество файлов в указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить количество файлов, включаемых в задание с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>См. также:

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
