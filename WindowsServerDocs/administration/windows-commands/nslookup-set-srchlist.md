---
title: nslookup set srchlist
description: Справочная статья по команде nslookup set срчлист, которая изменяет доменное имя и список поиска доменных имен (DNS) по умолчанию.
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de02663ce43b9f3f24f1addd739438a0796be0ea
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885491"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет доменное имя службы доменных имен (DNS) по умолчанию и список поиска. Эта команда переопределяет доменное имя DNS по умолчанию и список поиска команды [nslookup set domain](nslookup-set-domain.md) .

## <a name="syntax"></a>Синтаксис

```
set srchlist=<domainname>[/...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<domainname>` | Указывает новые имена для домена DNS по умолчанию и списка поиска. Значение доменного имени по умолчанию основано на имени узла. Можно указать не более шести имен, разделенных косыми чертами (/). |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

#### <a name="remarks"></a>Remarks

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
