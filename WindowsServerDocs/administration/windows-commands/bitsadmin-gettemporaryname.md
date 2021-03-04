---
title: bitsadmin gettemporaryname
description: Справочная статья по команде битсадмин жеттемпораринаме, которая сообщает о временном файле имени файла, указанного в задании.
ms.topic: reference
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 77c2e509f6c0c16005a794867ffeb85fa548c5a0
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821628"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname

Сообщает имя временного файла заданного файла в задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /gettemporaryname <job> <file_index>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| file_index | Начинается с 0. |

## <a name="examples"></a>Примеры

Чтобы сообщить о временном имени файла 2 для задания с именем *мидовнлоаджоб*:

```
bitsadmin /gettemporaryname myDownloadJob 1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
