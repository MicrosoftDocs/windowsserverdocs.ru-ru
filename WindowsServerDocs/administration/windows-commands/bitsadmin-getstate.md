---
title: bitsadmin getstate
description: Справочная статья по команде битсадминического состояния, которая получает состояние указанного задания.
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38ad3cedbd4dc9b0cc3d5e855ea4fabd1736b6aa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893842"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate

Возвращает состояние указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getstate <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

#### <a name="output"></a>Выходные данные

Возвращаемые выходные значения могут быть:

| Состояние | Описание |
| --------------- | ----------- |
| Поставлено в очередь | Задание ожидает запуска. |
| Соединение | Служба BITS свяжется с сервером. |
| Передача | BITS передает данные. |
| Передаются | Служба BITS успешно передала все файлы в задании. |
| Приостановлена | Задание приостановлено. |
| Ошибка | Произошла неустранимая ошибка; Повторная попытка перемещения не выполняется. |
| Transient_Error | Произошла устранимая ошибка; Повторная попытка передачи после истечения минимальной задержки. |
| Подтверждено | Задание завершено. |
| Отменено | Задание отменено. |

## <a name="examples"></a>Примеры

Чтобы получить состояние для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getstate myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
