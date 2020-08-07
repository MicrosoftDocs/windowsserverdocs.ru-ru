---
title: bitsadmin gettype
description: Справочная статья по команде битсадмин GetType, которая получает тип задания для указанного задания.
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f0fe66256e59526b874aaf2ec8ae0193846a1da
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893826"
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
