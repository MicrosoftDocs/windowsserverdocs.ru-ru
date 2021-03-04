---
title: bitsadmin getcreationtime
description: Справочная статья по команде битсадмин жеткреатионтиме, которая получает время создания для указанного задания.
ms.topic: reference
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 98fc49408e68365c1c6fbec3147c291cd6dfbe27
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822218"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

Извлекает время создания для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить время создания для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
