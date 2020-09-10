---
title: bitsadmin getreplydata
description: Справочная статья по команде битсадмин жетреплидата, которая получает данные отправки и ответа сервера в шестнадцатеричном формате для задания.
ms.topic: reference
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a15dc59d9487ed928954f8d5cbd47828c2b58291
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631720"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

Получает данные отправки и ответа сервера в шестнадцатеричном формате для задания.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getreplydata <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить данные отправки и ответа для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getreplydata myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
