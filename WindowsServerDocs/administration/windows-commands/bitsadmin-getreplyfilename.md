---
title: bitsadmin getreplyfilename
description: Справочная статья по команде битсадмин жетреплифиленаме, которая возвращает путь к файлу, содержащему сервер-ответ для задания.
ms.topic: reference
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: abbe4234841195faa6d7ece915d026ab51ba4422
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821668"
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
