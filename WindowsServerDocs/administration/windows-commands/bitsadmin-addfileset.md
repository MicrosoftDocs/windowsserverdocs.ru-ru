---
title: bitsadmin addfileset
description: Справочная статья по команде битсадмин аддфилесет, которая добавляет один или несколько файлов к указанному заданию.
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52a97817bd734a06ba787cb6faf17f2a03419da8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894917"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Добавляет один или несколько файлов к указанному заданию.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /addfileset <job> <textfile>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
