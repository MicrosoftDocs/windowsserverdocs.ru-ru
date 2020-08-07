---
title: bitsadmin getpriority
description: Справочная статья по команде битсадмин предшествовал, которая получает приоритет указанного задания.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 57d51e4a2a34fb5ae1361e864ee932ac314662b2
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894034"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

Возвращает приоритет указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
