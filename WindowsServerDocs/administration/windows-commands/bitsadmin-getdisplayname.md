---
title: bitsadmin getdisplayname
description: Справочная статья по команде битсадминического DisplayName, которая получает отображаемое имя указанного задания.
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ddc6e2f73062abca7c711a02c9c3a4f9c725bde
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894386"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

Извлекает отображаемое имя указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить отображаемое имя для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
