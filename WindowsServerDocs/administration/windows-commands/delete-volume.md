---
title: delete volume
description: Справочная статья по команде удаления тома, которая удаляет выбранный том.
ms.topic: reference
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d441aafd549a6e167751a2aa53685090d788fc30
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819048"
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