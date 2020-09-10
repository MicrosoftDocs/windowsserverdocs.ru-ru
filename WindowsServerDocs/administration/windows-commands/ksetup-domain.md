---
title: ksetup domain
description: Справочная статья по команде домена ksetup, которая задает доменное имя для всех операций Kerberos.
ms.topic: reference
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dcb7624f7b9fa81c66fed4533a0ba377095fa902
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640043"
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