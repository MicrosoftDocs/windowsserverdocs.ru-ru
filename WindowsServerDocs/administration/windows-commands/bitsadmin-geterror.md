---
title: bitsadmin geterror
description: Справочная статья по команде битсадмин Error, которая получает подробные сведения об ошибке для указанного задания.
ms.topic: reference
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9eb043b64d260f86bc98ba012eeddbb2181142f4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822077"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Извлекает подробные сведения об ошибке для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить сведения об ошибке для задания с именем *мидовнлоаджоб*:

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
