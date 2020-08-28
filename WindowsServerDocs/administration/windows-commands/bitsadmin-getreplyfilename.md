---
title: bitsadmin getreplyfilename
description: Справочная статья по команде битсадмин жетреплифиленаме, которая возвращает путь к файлу, содержащему сервер-ответ для задания.
ms.topic: reference
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c2e355bf0264c5dc995f0d241afe7b641d2a41b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034882"
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
