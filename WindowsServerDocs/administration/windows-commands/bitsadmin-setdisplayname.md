---
title: bitsadmin setdisplayname
description: Справочная статья по команде битсадмин сетдисплайнаме, которая задает отображаемое имя указанного задания.
ms.topic: reference
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4726d4d1dec867e72ab542222a71289994ed12fd
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028542"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Задает отображаемое имя для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| display_name | Текст, используемый в качестве отображаемого имени для конкретного задания. |

## <a name="examples"></a>Примеры

Чтобы задать отображаемое имя для задания *мидовнлоаджоб*, сделайте следующее:

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
