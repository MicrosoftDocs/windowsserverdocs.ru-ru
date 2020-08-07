---
title: ksetup setrealm
description: Справочная статья по команде ksetup сетреалм, которая задает имя области Kerberos.
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 501660d072cdb651a26098f8ac63cee21dfcba88
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887721"
---
# <a name="ksetup-setrealm"></a>ksetup setrealm

Задает имя области Kerberos.

> [!IMPORTANT]
> Установка области Kerberos на контроллере домена не поддерживается. Попытка сделать это вызовет предупреждение и сбой команды.

## <a name="syntax"></a>Синтаксис

```
ksetup /setrealm <DNSdomainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<DNSdomainname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. Можно использовать полное доменное имя или простую форму имени. Если вы не используете прописные буквы в качестве DNS-имени, вам будет предложено выполнить проверку, чтобы продолжить. |

### <a name="examples"></a>Примеры

Чтобы задать для области этого компьютера определенное доменное имя и ограничить доступ неконтроллером домена только к сфере CONTOSO Kerberos, введите:

```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup removerealm](ksetup-removerealm.md)
