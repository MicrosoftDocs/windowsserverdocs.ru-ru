---
title: bitsadmin getcreationtime
description: Справочная статья по команде битсадмин жеткреатионтиме, которая получает время создания для указанного задания.
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42cd6de0769d4a741e76a1f6b03c32123ea8cf6a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894453"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

Извлекает время создания для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
