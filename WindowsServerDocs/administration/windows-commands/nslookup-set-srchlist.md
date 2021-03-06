---
title: nslookup set srchlist
description: Справочная статья по команде nslookup set срчлист, которая изменяет доменное имя и список поиска доменных имен (DNS) по умолчанию.
ms.topic: reference
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 410a608f9caf5a17a61bcb1ef976042848623dde
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101809750"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет доменное имя службы доменных имен (DNS) по умолчанию и список поиска. Эта команда переопределяет доменное имя DNS по умолчанию и список поиска команды [nslookup set domain](nslookup-set-domain.md) .

## <a name="syntax"></a>Синтаксис

```
set srchlist=<domainname>[/...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<domainname>` | Указывает новые имена для домена DNS по умолчанию и списка поиска. Значение доменного имени по умолчанию основано на имени узла. Можно указать не более шести имен, разделенных косыми чертами (/). |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Используйте команду [nslookup set ALL](nslookup-set-all.md) , чтобы отобразить список.

### <a name="examples"></a>Примеры

Чтобы задать для домена DNS значение *Mfg.widgets.com* , а в списке поиска — три имени:

```
set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set domain](nslookup-set-domain.md)

- [nslookup set all](nslookup-set-all.md)
