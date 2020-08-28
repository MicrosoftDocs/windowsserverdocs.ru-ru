---
title: delete volume
description: Справочная статья по команде удаления тома, которая удаляет выбранный том.
ms.topic: reference
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c88834b800414bcf3ff246272ec187fb98d47db
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024158"
---
# <a name="delete-volume"></a>delete volume

Удаляет выбранный том. Прежде чем начать, необходимо выбрать том для выполнения этой операции. Используйте команду [выбрать том](select-volume.md) , чтобы выбрать том и переместить фокус на него.

> [!IMPORTANT]
> Нельзя удалить системный том, загрузочный том или любой том, содержащий активный файл подкачки или аварийный дамп (дамп памяти).

## <a name="syntax"></a>Синтаксис

```
delete volume [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="examples"></a>Примеры

Чтобы удалить том с фокусом, введите:

```
delete volume
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [select volume](select-volume.md)

- [удалить команду](delete.md)