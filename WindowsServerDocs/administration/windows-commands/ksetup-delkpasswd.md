---
title: ksetup delkpasswd
description: Справочная статья по команде ksetup делкпассвд, которая удаляет сервер паролей Kerberos (кпассвд) для области.
ms.topic: reference
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 52624252953770ebe131a7c31618058232a21d05
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639679"
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
