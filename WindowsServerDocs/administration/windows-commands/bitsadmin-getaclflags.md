---
title: bitsadmin getaclflags
description: Справочная статья по команде битсадмин жетаклфлагс, которая получает флаги распространения списка управления доступом (ACL).
ms.topic: reference
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4c5c7101db157b7fa5b56833b8d5f89619bd8d51
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632320"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

Извлекает флаги распространения списка управления доступом (ACL), отражающие наследование элементов дочерними объектами.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getaclflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

### <a name="remarks"></a>Примечания

Возвращает одно или несколько из следующих значений флагов:

- **o** — копирование сведений о владельце с помощью файла.

- **g** — копирование сведений о группе с помощью файла.

- **d** — копирование сведений о избирательном списке управления доступом (DACL) с помощью файла.

- **s** -копирование данных системного списка управления доступом (SACL) с помощью файла.

## <a name="examples"></a>Примеры

Чтобы получить флаги распространения списка управления доступом для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getaclflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
