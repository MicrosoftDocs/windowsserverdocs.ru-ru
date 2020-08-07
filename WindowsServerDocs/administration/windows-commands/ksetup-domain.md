---
title: ksetup domain
description: Справочная статья по команде домена ksetup, которая задает доменное имя для всех операций Kerberos.
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81135ed668da901c55e891cec4c8749687359818
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887935"
---
# <a name="ksetup-domain"></a>ksetup domain

Задает доменное имя для всех операций Kerberos.

## <a name="syntax"></a>Синтаксис

```
ksetup /domain <domainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<domainname>` | Имя домена, для которого требуется установить соединение. Используйте полное доменное имя или простую форму имени, например contoso.com или contoso.|

### <a name="examples"></a>Примеры

Чтобы установить подключение к допустимому домену, такому как Microsoft, с помощью `ksetup /mapuser` подкоманды, введите:

```
ksetup /mapuser principal@realm domain-user /domain domain-name
```

После успешного подключения вы получите новый TGT или обновите существующий TGT.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup мапусер, команда](ksetup-mapuser.md)