---
title: ksetup setenctypeattr
description: Справочная статья по команде ksetup сетенктипеаттр, которая задает атрибут типа шифрования для домена.
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50d5c5be2382cc1d811066d577f8f092b676853a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887768"
---
# <a name="ksetup-setenctypeattr"></a>ksetup setenctypeattr

Задает атрибут типа шифрования для домена. Сообщение о состоянии отображается при успешном или неудачном завершении.

Вы можете просмотреть тип шифрования для билета предоставления билета Kerberos (TGT) и ключ сеанса, выполнив команду **klist** и просмотрев выходные данные. Вы можете задать домен для подключения и использования, выполнив `ksetup /domain <domainname>` команду.

## <a name="syntax"></a>Синтаксис

```
ksetup /setenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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

Чтобы задать для атрибута типа шифрования значение AES-256-CTS-HMAC-SHA1-96 для домена corp.contoso.com, введите:

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

- [ksetup адденктипеаттр, команда](ksetup-addenctypeattr.md)

- [ksetup жетенктипеаттр, команда](ksetup-getenctypeattr.md)

- [ksetup деленктипеаттр, команда](ksetup-delenctypeattr.md)
