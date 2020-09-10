---
title: bitsadmin getnotifycmdline
description: Справочная статья по команде битсадмин жетнотификмдлине, которая получает команду командной строки, которая выполняется, когда задание завершает передачу данных.
ms.topic: reference
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 26b2f50520f0b77f5792b279513caedaf560eea9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631922"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

Получает команду командной строки, которая будет запускаться после завершения передачи данных указанным заданием.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Для получения команды командной строки, используемой службой при завершении задания с именем *мидовнлоаджоб* .

```
bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
