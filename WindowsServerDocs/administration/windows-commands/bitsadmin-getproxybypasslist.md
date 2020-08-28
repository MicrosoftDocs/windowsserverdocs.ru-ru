---
title: bitsadmin getproxybypasslist
description: Справочная статья по команде битсадмин жетпроксибипасслист, которая получает список обхода прокси-сервера для указанного задания.
ms.topic: reference
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb767ce9201b8c652df52a9049ce474ec8d8ea2e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028652"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

Извлекает список обхода прокси-сервера для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
