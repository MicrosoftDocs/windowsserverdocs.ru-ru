---
title: bitsadmin getreplyfilename
description: Справочная статья по команде битсадмин жетреплифиленаме, которая возвращает путь к файлу, содержащему сервер-ответ для задания.
ms.topic: reference
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d3dab8e7f2a50c00c1c5ccb72f4e6dea76df3090
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631710"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

Возвращает путь к файлу, содержащему сервер-ответ для задания.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getreplyfilename <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить имя файла для отправки и ответа для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getreplyfilename myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
