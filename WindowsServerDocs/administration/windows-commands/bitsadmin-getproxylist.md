---
title: битсадмин жетпроксилист — извлекает список прокси-серверов для указанного задания.
description: Справочная статья по команде битсадмин жетпроксилист, которая получает список прокси-серверов для указанного задания.
ms.topic: reference
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9038f9faaedce30bfdf6025a40e3f6369805ac2a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024418"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Извлекает разделенный запятыми список прокси-серверов, используемых для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
