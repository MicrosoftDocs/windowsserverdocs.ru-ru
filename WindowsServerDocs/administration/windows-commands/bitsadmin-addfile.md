---
title: bitsadmin addfile
description: Справочная статья по команде битсадмин AddFile, которая добавляет файл к указанному заданию.
ms.topic: reference
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 80d4a77da8619c39909d31ff4a29f76375c46ac9
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822638"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

Добавляет файл в указанное задание.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /addfile <job> <remoteURL> <localname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| ремотеурл | URL-адрес файла на сервере. |
| localname | Имя файла на локальном компьютере. *LocalName* должно содержать абсолютный путь к файлу. |

## <a name="examples"></a>Примеры

Чтобы добавить файл в задание, выполните следующие действия.

```
bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

Повторите этот вызов для каждого добавляемого файла. Если несколько заданий используют *мидовнлоаджоб* в качестве имени, необходимо заменить *мидовнлоаджоб* на GUID задания для уникальной идентификации задания.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
