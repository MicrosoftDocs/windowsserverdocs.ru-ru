---
title: nslookup set type
description: Справочная статья по команде nslookup set Type, которая изменяет тип записи ресурса для запроса.
ms.topic: article
ms.assetid: 5248e314-fac1-413e-81dc-bbe0a0873ba5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b339f5dc809df1ad9f3301108169c65b02e63309
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885460"
---
# <a name="nslookup-set-type"></a>nslookup set type

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет тип записи ресурса для запроса. Дополнительные сведения о типах записей ресурсов см. в статье [запрос комментария (RFC) 1035](https://tools.ietf.org/html/rfc1035).

> [!NOTE]
> Эта команда аналогична команде [nslookup set QueryType](nslookup-set-querytype.md) .

## <a name="syntax"></a>Синтаксис

```
set type=<resourcerecordtype>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<resourcerecordtype>` | Указывает тип записи ресурса DNS. Тип записи ресурса по умолчанию **—, но**можно использовать любое из следующих значений:<ul><li>Ответ **.** Указывает IP-адрес компьютера.</li><li>**Все:** Указывает IP-адрес компьютера.</li><li>**Запись CNAME:** Задает каноническое имя для псевдонима.</li><li>**GID** Задает идентификатор группы для имени группы.</li><li>**HINFO:** Указывает процессор и тип операционной системы компьютера.</li><li>**МБ:** Указывает доменное имя почтового ящика.</li><li>**MG:** Указывает члена почтовой группы.</li><li>**MINFO:** Указывает сведения о почтовом ящике или списке рассылки.</li><li>**Mr:** Указывает имя домена переименования почты.</li><li>**MX:** Указывает почтовый обменник.</li><li>**Ns:** Указывает сервер DNS-имен для именованной зоны.</li><li>**Ptr:** Указывает имя компьютера, если запрос является IP-адресом; в противном случае указывает указатель на другую информацию.</li><li>**SOA:** Указывает начальную зону для зоны DNS.</li><li>**Txt:** Задает текстовую информацию.</li><li>**UID:** Указывает идентификатор пользователя.</li><li>**Уинфо:** Указывает сведения о пользователе.</li><li>**WKS:** Описание хорошо известной службы.</li></ul> |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-querytype.md)
