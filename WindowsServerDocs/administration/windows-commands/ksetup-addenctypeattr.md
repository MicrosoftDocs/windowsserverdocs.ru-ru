---
title: ksetup addenctypeattr
description: Справочная статья по команде ksetup адденктипеаттр, которая добавляет атрибут типа шифрования в список возможных типов для домена.
ms.topic: reference
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a49780a7a229c1c30d827632b1a6d71584f09c6
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037712"
---
# <a name="ksetup-addenctypeattr"></a>ksetup addenctypeattr

Добавляет атрибут типа шифрования в список возможных типов для домена. Сообщение о состоянии отображается при успешном или неудачном завершении.

## <a name="syntax"></a>Синтаксис

```
ksetup /addenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<domainname>` | Имя домена, для которого требуется установить соединение. Используйте полное доменное имя или простую форму имени, например corp.contoso.com или contoso. |
| тип шифрования | Должен быть одним из следующих поддерживаемых типов шифрования:<ul><li>DES-CBC-CRC</li><li>DES-CBC-MD5</li><li>RC4-HMAC-MD5</li><li>AES128-CTS-HMAC-SHA1-96</li><li>AES256-CTS-HMAC-SHA1-96</li></ul> |

#### <a name="remarks"></a>Remarks

- Можно задать или добавить несколько типов шифрования, разделяя типы шифрования в команде пробелами. Однако это можно сделать только для одного домена за раз.

### <a name="examples"></a>Примеры

Чтобы просмотреть тип шифрования билета предоставления билета Kerberos (TGT) и ключа сеанса, введите:

```
klist
```

Чтобы задать для домена значение corp.contoso.com, введите:

```
ksetup /domain corp.contoso.com
```

Чтобы добавить тип шифрования *AES-256-CTS-HMAC-SHA1-96* в список возможных типов для домена *Corp.contoso.com*, введите:

```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Чтобы задать для атрибута типа шифрования значение *AES-256-CTS-HMAC-SHA1-96* для домена *Corp.contoso.com*, введите:

```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Чтобы убедиться, что атрибут типа шифрования был задан в качестве назначения для домена, введите:

```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда klist](klist.md)

- [Команда ksetup](ksetup.md)

- [Команда домена ksetup](ksetup-domain.md)

- [ksetup сетенктипеаттр, команда](ksetup-setenctypeattr.md)

- [ksetup жетенктипеаттр, команда](ksetup-getenctypeattr.md)

- [ksetup деленктипеаттр, команда](ksetup-delenctypeattr.md)
