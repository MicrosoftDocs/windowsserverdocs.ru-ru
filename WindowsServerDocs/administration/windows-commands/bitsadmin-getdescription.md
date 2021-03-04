---
title: bitsadmin getdescription
description: Справочная статья по команде битсадмин Description, которая получает описание указанного задания.
ms.topic: reference
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 806209371e994c0f1db1473778f0155b24ad53c2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822178"
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
