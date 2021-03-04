---
title: битсадмин жетпроксилист — извлекает список прокси-серверов для указанного задания.
description: Справочная статья по команде битсадмин жетпроксилист, которая получает список прокси-серверов для указанного задания.
ms.topic: reference
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8c96208a036847690c60a00f48dc4201c9d21ff1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821778"
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
