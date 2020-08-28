---
title: bitsadmin getcreationtime
description: Справочная статья по команде битсадмин жеткреатионтиме, которая получает время создания для указанного задания.
ms.topic: reference
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1175b148e0169f5b8f76d66ae3358a1069f5c4f7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030432"
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
