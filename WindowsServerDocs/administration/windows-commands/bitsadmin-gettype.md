---
title: bitsadmin gettype
description: Справочная статья по команде битсадмин GetType, которая получает тип задания для указанного задания.
ms.topic: reference
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ccb938e1fe67164567bbe8d6c87d87423026db96
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631561"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

Возвращает тип задания для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

#### <a name="output"></a>Выходные данные

Возвращаемые выходные значения могут быть:

| Тип | Описание |
| --------------- | ----------- |
| Скачивание | Задание является загружаемым. |
| Передать | Задание — это отправка. |
| Отправка и ответ | Задание представляет собой отправку и ответ. |
| Неизвестно | Задание имеет неизвестный тип. |

## <a name="examples"></a>Примеры

Чтобы получить тип задания для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
