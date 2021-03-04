---
title: bitsadmin getdisplayname
description: Справочная статья по команде битсадминического DisplayName, которая получает отображаемое имя указанного задания.
ms.topic: reference
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 888df4279df1ce4654c3990f6bd67bf2125d2b5f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822158"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

Извлекает отображаемое имя указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
