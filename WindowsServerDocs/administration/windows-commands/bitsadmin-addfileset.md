---
title: bitsadmin addfileset
description: Справочная статья по команде битсадмин аддфилесет, которая добавляет один или несколько файлов к указанному заданию.
ms.topic: reference
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e3e736fe6dcc96b7f81b3b249257f0d23dd78c9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632717"
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
