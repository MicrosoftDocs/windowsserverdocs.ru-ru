---
title: ksetup domain
description: Справочная статья по команде домена ksetup, которая задает доменное имя для всех операций Kerberos.
ms.topic: reference
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9b92fcc0afccff9cbc5de24b2244c180c85da2f1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101815118"
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