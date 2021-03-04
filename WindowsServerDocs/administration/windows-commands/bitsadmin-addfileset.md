---
title: bitsadmin addfileset
description: Справочная статья по команде битсадмин аддфилесет, которая добавляет один или несколько файлов к указанному заданию.
ms.topic: reference
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4cf0ecda90c8248277fb7c23c8cefd1548b56262
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822628"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Добавляет один или несколько файлов к указанному заданию.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| textfile | Текстовый файл, каждая строка которого содержит удаленное и локальное имя файла. **Примечание.** Имена должны быть разделены пробелами. Строки, начинающиеся с `#` символа, обрабатываются как комментарии. |

## <a name="examples"></a>Примеры

```
bitsadmin /addfileset files.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
