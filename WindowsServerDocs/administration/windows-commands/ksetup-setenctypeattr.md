---
title: ksetup setenctypeattr
description: Справочная статья по команде ksetup сетенктипеаттр, которая задает атрибут типа шифрования для домена.
ms.topic: reference
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9027197817b2fa738726fd0d0feeeeadc5aac0b2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634124"
---
# <a name="ksetup-setenctypeattr"></a>ksetup setenctypeattr

Задает атрибут типа шифрования для домена. Сообщение о состоянии отображается при успешном или неудачном завершении.

Вы можете просмотреть тип шифрования для билета предоставления билета Kerberos (TGT) и ключ сеанса, выполнив команду **klist** и просмотрев выходные данные. Вы можете задать домен для подключения и использования, выполнив `ksetup /domain <domainname>` команду.

## <a name="syntax"></a>Синтаксис

```
ksetup /setenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<domainname>` | Имя домена, для которого требуется установить соединение. Используйте полное доменное имя или простую форму имени, например corp.contoso.com или contoso. |
| тип шифрования | Должен быть одним из следующих поддерживаемых типов шифрования:<ul><li>DES-CBC-CRC</li><li>DES-CBC-MD5</li><li>RC4-HMAC-MD5</li><li>AES128-CTS-HMAC-SHA1-96</li><li>AES256-CTS-HMAC-SHA1-96</li></ul> |

#### <a name="remarks"></a>Примечания

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
