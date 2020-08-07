---
title: bitsadmin gettemporaryname
description: Справочная статья по команде битсадмин жеттемпораринаме, которая сообщает о временном файле имени файла, указанного в задании.
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b5919d45f2b8497bb6e8fa6cf3650f49e27cd48
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893837"
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
