---
title: bitsadmin getbytestotal
description: Справочная статья по команде битсадмин жетбитестотал, которая получает размер указанного задания.
ms.topic: reference
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a8496234c0907061997ddd790e03f78d84c5380
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024428"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

Возвращает размер указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить размер задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
