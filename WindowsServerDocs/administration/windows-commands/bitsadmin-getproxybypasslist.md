---
title: bitsadmin getproxybypasslist
description: Справочная статья по команде битсадмин жетпроксибипасслист, которая получает список обхода прокси-сервера для указанного задания.
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16cca14a47f086be65764da5441d915d2d28d2db
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894006"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

Извлекает список обхода прокси-сервера для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

### <a name="remarks"></a>Remarks

Список обхода содержит имена узлов или IP-адреса, которые не направляются через прокси-сервер. Список может содержать `<local>` ссылки на все серверы в одной локальной сети. Список может быть точкой с запятой (;) или с разделителями-пробелами.

## <a name="examples"></a>Примеры

Чтобы получить список обхода прокси-сервера для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
