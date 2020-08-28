---
title: bitsadmin listfiles
description: Справочная статья по команде битсадмин листфилес, в которой перечислены файлы в указанном задании.
ms.topic: reference
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b6afadf78acd187b336484db47b128afb49e27fe
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024308"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Перечисляет файлы в указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить список файлов для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
