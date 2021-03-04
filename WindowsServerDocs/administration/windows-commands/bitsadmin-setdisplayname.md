---
title: bitsadmin setdisplayname
description: Справочная статья по команде битсадмин сетдисплайнаме, которая задает отображаемое имя указанного задания.
ms.topic: reference
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8531e3c10396a75983f32640a6e5a7b309820357
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820998"
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
