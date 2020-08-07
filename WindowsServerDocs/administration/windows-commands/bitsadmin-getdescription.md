---
title: bitsadmin getdescription
description: Справочная статья по команде битсадмин Description, которая получает описание указанного задания.
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5023a0a4114796fa3a492de4fddaa0d5ddb0187
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894406"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

Извлекает описание указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить описание задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getdescription myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
