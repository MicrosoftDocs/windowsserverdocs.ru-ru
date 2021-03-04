---
title: bitsadmin gettype
description: Справочная статья по команде битсадмин GetType, которая получает тип задания для указанного задания.
ms.topic: reference
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b79c0a1615f02db4401f78339f216395a2b44799
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821598"
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
| Скачать | Задание является загружаемым. |
| Передать | Задание — это отправка. |
| Upload-Reply | Задание представляет собой отправку и ответ. |
| Неизвестно | Задание имеет неизвестный тип. |

## <a name="examples"></a>Примеры

Чтобы получить тип задания для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
