---
title: bitsadmin getproxybypasslist
description: Справочная статья по команде битсадмин жетпроксибипасслист, которая получает список обхода прокси-сервера для указанного задания.
ms.topic: reference
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e116a417c2c8a2970daaf229ec1fe76c21cc40aa
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821788"
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

### <a name="remarks"></a>Комментарии

Список обхода содержит имена узлов или IP-адреса, которые не направляются через прокси-сервер. Список может содержать `<local>` ссылки на все серверы в одной локальной сети. Список может быть точкой с запятой (;) или с разделителями-пробелами.

## <a name="examples"></a>Примеры

Чтобы получить список обхода прокси-сервера для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
