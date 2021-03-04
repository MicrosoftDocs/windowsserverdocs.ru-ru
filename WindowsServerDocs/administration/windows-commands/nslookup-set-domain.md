---
title: nslookup set domain
description: Справочная статья по команде nslookup set domain, которая изменяет доменное имя DNS по умолчанию на указанное имя.
ms.topic: reference
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6e42167dde4f7d42d7961279358ecea7125a27f5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101809932"
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

#### <a name="remarks"></a>Комментарии

- Доменное имя DNS по умолчанию добавляется к поисковому запросу в зависимости от состояния параметров **дефнаме** и **поиска** .

- Список поиска доменов DNS содержит родительские домены DNS по умолчанию, если в имени содержится по крайней мере два компонента. Например, если домен DNS по умолчанию — mfg.widgets.com, список поиска будет называться как mfg.widgets.com, так и widgets.com.

- Используйте команду [nslookup set срчлист](nslookup-set-srchlist.md) , чтобы указать другой список, и команда [nslookup set ALL](nslookup-set-all.md) будет отображать список.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set srchlist](nslookup-set-srchlist.md)

- [nslookup set all](nslookup-set-all.md)
