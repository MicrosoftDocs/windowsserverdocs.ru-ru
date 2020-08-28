---
title: ksetup delkpasswd
description: Справочная статья по команде ksetup делкпассвд, которая удаляет сервер паролей Kerberos (кпассвд) для области.
ms.topic: reference
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8918b429bc29cd2eec88f5c32d1e0c358fa2610
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025568"
---
# <a name="ksetup-delkpasswd"></a>ksetup delkpasswd

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет сервер паролей Kerberos (кпассвд) для области.

## <a name="syntax"></a>Синтаксис

```
ksetup /delkpasswd <realmname> <kpasswdname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<realmname>` |  Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM и указывается в качестве области по умолчанию или **области =** при запуске **ksetup** . |
| `<kpasswdname>` | Указывает сервер паролей Kerberos. Оно называется без учета регистра, полное доменное имя, например mitkdc.contoso.com. Если имя KDC пропущено, для размещения Кдкс может использоваться DNS. |

### <a name="examples"></a>Примеры

Чтобы убедиться в наличии сферы CORP. CONTOSO.COM использует сервер Windows Server KDC, отличный от mitkdc.contoso.com, в качестве сервера паролей введите:

```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

Чтобы убедиться в наличии сферы CORP. CONTOSO.COM не сопоставляется с сервером паролей Kerberos (имя KDC), введите `ksetup` на компьютере Windows и просмотрите выходные данные.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup делкпассвд, команда](ksetup-delkpasswd.md)
