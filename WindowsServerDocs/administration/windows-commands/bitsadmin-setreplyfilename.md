---
title: bitsadmin setreplyfilename
description: Справочная статья по команде битсадмин сетреплифиленаме, которая указывает путь к файлу, содержащему сервер отправка-ответ.
ms.topic: reference
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3fb3144119029e3e48fae16a128016f128582248
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820788"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

Указывает путь к файлу, содержащему сервер отправка-ответ.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setreplyfilename <job> <file_path>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| file_path | Расположение для отправки и ответа сервера. |

## <a name="examples"></a>Примеры

Чтобы задать путь к файлу имени файла для задания upload-Reply, выполните команду с именем *мидовнлоаджоб*:

```
bitsadmin /setreplyfilename myDownloadJob c:\upload-reply
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
