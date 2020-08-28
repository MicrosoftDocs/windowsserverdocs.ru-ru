---
title: nslookup set domain
description: Справочная статья по команде nslookup set domain, которая изменяет доменное имя DNS по умолчанию на указанное имя.
ms.topic: reference
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed002a7a6278d9bcd11a59c5708c723d7ffe91ef
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023448"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет доменное имя DNS по умолчанию на указанное имя.

## <a name="syntax"></a>Синтаксис

```
set domain=<domainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<domainname>` | Указывает новое имя для доменного имени DNS по умолчанию. Значение по умолчанию — имя узла. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

#### <a name="remarks"></a>Remarks

- Доменное имя DNS по умолчанию добавляется к поисковому запросу в зависимости от состояния параметров **дефнаме** и **поиска** .

- Список поиска доменов DNS содержит родительские домены DNS по умолчанию, если в имени содержится по крайней мере два компонента. Например, если домен DNS по умолчанию — mfg.widgets.com, список поиска будет называться как mfg.widgets.com, так и widgets.com.

- Используйте команду [nslookup set срчлист](nslookup-set-srchlist.md) , чтобы указать другой список, и команда [nslookup set ALL](nslookup-set-all.md) будет отображать список.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set srchlist](nslookup-set-srchlist.md)

- [nslookup set all](nslookup-set-all.md)
