---
title: bitsadmin setcustomheaders
description: Справочная статья по команде битсадмин сеткустомхеадерс, которая добавляет пользовательский заголовок HTTP к запросу GET.
ms.topic: reference
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84622cba8bb2bcb6a9ebfe782fdadc33a388fdb2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031282"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

Добавьте пользовательский заголовок HTTP в запрос GET, отправляемый на HTTP-сервер. Дополнительные сведения о запросах GET см. в разделе [определения методов](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) и [определения полей заголовка](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| `<header1> <header2>` и т. д. | Пользовательские заголовки для задания. |

## <a name="examples"></a>Примеры

Чтобы добавить пользовательский заголовок HTTP для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
