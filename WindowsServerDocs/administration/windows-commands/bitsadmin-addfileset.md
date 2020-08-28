---
title: bitsadmin addfileset
description: Справочная статья по команде битсадмин аддфилесет, которая добавляет один или несколько файлов к указанному заданию.
ms.topic: reference
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b9b93f38f3604c4f0a9fcaf886d74356d355086
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033712"
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
