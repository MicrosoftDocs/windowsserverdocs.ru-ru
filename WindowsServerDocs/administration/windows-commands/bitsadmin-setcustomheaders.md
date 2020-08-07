---
title: bitsadmin setcustomheaders
description: Справочная статья по команде битсадмин сеткустомхеадерс, которая добавляет пользовательский заголовок HTTP к запросу GET.
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 407e4aa85d8413167add716cd63fe620f73b0e12
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893183"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

Добавьте пользовательский заголовок HTTP в запрос GET, отправляемый на HTTP-сервер. Дополнительные сведения о запросах GET см. в разделе [определения методов](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) и [определения полей заголовка](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| `<header1> <header2>`и т. д. | Пользовательские заголовки для задания. |

## <a name="examples"></a>Примеры

Чтобы добавить пользовательский заголовок HTTP для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
