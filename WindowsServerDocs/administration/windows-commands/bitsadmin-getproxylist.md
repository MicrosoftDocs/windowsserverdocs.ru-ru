---
title: битсадмин жетпроксилист — извлекает список прокси-серверов для указанного задания.
description: Справочная статья по команде битсадмин жетпроксилист, которая получает список прокси-серверов для указанного задания.
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bcd94c65a11006a795f071224397d8b3081b7548
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893975"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Извлекает разделенный запятыми список прокси-серверов, используемых для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить список прокси-серверов для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
