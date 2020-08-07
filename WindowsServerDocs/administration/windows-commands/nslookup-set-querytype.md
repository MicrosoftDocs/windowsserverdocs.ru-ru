---
title: nslookup set querytype
description: Справочная статья по команде nslookup set QueryType, которая изменяет тип записи ресурса для запроса.
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9319b5e7de8b31d805114b9d70c9700ee2a033ac
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885636"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет тип записи ресурса для запроса. Дополнительные сведения о типах записей ресурсов см. в статье [запрос комментария (RFC) 1035](https://tools.ietf.org/html/rfc1035).

> [!NOTE]
> Эта команда аналогична команде [nslookup set Type](nslookup-set-type.md) .

## <a name="syntax"></a>Синтаксис

```
set querytype=<resourcerecordtype>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<resourcerecordtype>` | Указывает тип записи ресурса DNS. Тип записи ресурса по умолчанию **—, но**можно использовать любое из следующих значений:<ul><li>Ответ **.** Указывает IP-адрес компьютера.</li><li>**Все:** Указывает IP-адрес компьютера.</li><li>**Запись CNAME:** Задает каноническое имя для псевдонима.</li><li>**GID** Задает идентификатор группы для имени группы.</li><li>**HINFO:** Указывает процессор и тип операционной системы компьютера.</li><li>**МБ:** Указывает доменное имя почтового ящика.</li><li>**MG:** Указывает члена почтовой группы.</li><li>**MINFO:** Указывает сведения о почтовом ящике или списке рассылки.</li><li>**Mr:** Указывает имя домена переименования почты.</li><li>**MX:** Указывает почтовый обменник.</li><li>**Ns:** Указывает сервер DNS-имен для именованной зоны.</li><li>**Ptr:** Указывает имя компьютера, если запрос является IP-адресом; в противном случае указывает указатель на другую информацию.</li><li>**SOA:** Указывает начальную зону для зоны DNS.</li><li>**Txt:** Задает текстовую информацию.</li><li>**UID:** Указывает идентификатор пользователя.</li><li>**Уинфо:** Указывает сведения о пользователе.</li><li>**WKS:** Описание хорошо известной службы.</li></ul> |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-type.md)
