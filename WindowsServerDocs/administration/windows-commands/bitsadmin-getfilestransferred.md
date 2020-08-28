---
title: bitsadmin getfilestransferred
description: Справочная статья по команде битсадмин жетфилестрансферред, которая получает количество файлов, переданных для указанного задания.
ms.topic: reference
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e86e35d80e8e6b00d973b60e314f22068f7d115b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033592"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

Возвращает количество файлов, переданных для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить количество файлов, переданных в задании с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
