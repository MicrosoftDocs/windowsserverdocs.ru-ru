---
title: bitsadmin getpriority
description: Справочная статья по команде битсадмин предшествовал, которая получает приоритет указанного задания.
ms.topic: reference
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 3cb8f33f691e1cadf55d2013d75ced6834a1feee
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821798"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

Возвращает приоритет указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

#### <a name="output"></a>Выходные данные

Для этой команды может быть возвращен следующий приоритет:

- **ПЕРЕДНЕГО плана**

- **ВЫСОКОМ**

- **ОБЫЧНО**

- **НИЗШУЮ**

- **UNKNOWN**

## <a name="examples"></a>Примеры

Чтобы получить приоритет для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
