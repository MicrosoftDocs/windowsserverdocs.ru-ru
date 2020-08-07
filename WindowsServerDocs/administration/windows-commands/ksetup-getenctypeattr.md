---
title: ksetup getenctypeattr
description: Справочная статья по команде ksetup жетенктипеаттр, которая получает атрибут типа шифрования для домена.
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27dfd66e5108aa4704b999671397cb90049d1a15
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887909"
---
# <a name="ksetup-getenctypeattr"></a>ksetup getenctypeattr

Извлекает атрибут типа шифрования для домена. Сообщение о состоянии отображается при успешном или неудачном завершении.

Вы можете просмотреть тип шифрования для билета предоставления билета Kerberos (TGT) и ключ сеанса, выполнив команду **klist** и просмотрев выходные данные. Вы можете задать домен для подключения и использования, выполнив `ksetup /domain <domainname>` команду.

## <a name="syntax"></a>Синтаксис

```
ksetup /getenctypeattr <domainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<domainname>` | Имя домена, для которого требуется установить соединение. Используйте полное доменное имя или простую форму имени, например corp.contoso.com или contoso. |

### <a name="examples"></a>Примеры

Чтобы проверить атрибут типа шифрования для домена, введите:

```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда klist](klist.md)

- [Команда ksetup](ksetup.md)

- [Команда домена ksetup](ksetup-domain.md)

- [ksetup адденктипеаттр, команда](ksetup-addenctypeattr.md)

- [ksetup сетенктипеаттр, команда](ksetup-setenctypeattr.md)

- [ksetup деленктипеаттр, команда](ksetup-delenctypeattr.md)
