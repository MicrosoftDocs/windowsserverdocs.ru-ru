---
title: bitsadmin getbytestotal
description: Справочная статья по команде битсадмин жетбитестотал, которая получает размер указанного задания.
ms.topic: reference
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 50b926b8d89e402ef4fd9e58896963edd3c368c9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632346"
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
