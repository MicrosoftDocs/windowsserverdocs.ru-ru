---
title: ksetup listrealmflags
description: Справочная статья по команде ksetup листреалмфлагс, в которой перечислены доступные флаги области, которые можно сообщить по ksetup.
ms.topic: reference
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ddbc7f2421fc9c4acfcb38d0e83776f550908e28
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640026"
---
# <a name="ksetup-listrealmflags"></a>ksetup listrealmflags

Список доступных флагов области, которые могут быть переданы по **ksetup**.

## <a name="syntax"></a>Синтаксис

```
ksetup /listrealmflags
```

### <a name="remarks"></a>Примечания

- Флаги сферы задают дополнительные возможности области Kerberos, которые не основаны на операционной системе Windows Server. Компьютеры под управлением Windows Server могут использовать сервер Kerberos для администрирования проверки подлинности в области Kerberos вместо использования домена под управлением операционной системы Windows Server. Эта запись устанавливает функции области и имеет следующие значения:

| Значение | Флаг области | Описание |
| ----- | ---------- | ----------- |
| 0xF | Все | Заданы все флаги сферы. |
| 0x00 | Нет | Флаги области не заданы, а дополнительные функции не включены. |
| 0x01 | сендаддресс | IP-адрес будет включаться в билеты предоставления билетов. |
| 0x02 | ткпсуппортед | В этой области поддерживаются протоколы TCP и UDP (User Datagram Protocol). |
| 0x04 | delegate | Все пользователи в этой области являются доверенными для делегирования. |
| 0x08 | нксуппортед | Эта область поддерживает канонизации имен, что позволяет использовать стандарты именования DNS и областей. |
| 0x80 | RC4 | Эта область поддерживает шифрование RC4 для включения доверительных отношений между сферами, что позволяет использовать TLS. |

- Флаги сферы хранятся в реестре в разделе `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` . Эта запись не существует в реестре по умолчанию. Для заполнения реестра можно использовать [команду ksetup аддреалмфлагс](ksetup-addrealmflags.md) .

## <a name="examples"></a>Примеры

Чтобы получить список известных флагов области на этом компьютере, введите:

```
ksetup /listrealmflags
```

Чтобы установить доступные флаги области, которые **ksetup** не знает, введите:

```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```

**Ни**

```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup аддреалмфлагс, команда](ksetup-addrealmflags.md)

- [ksetup сетреалмфлагс, команда](ksetup-setrealmflags.md)

- [ksetup делреалмфлагс, команда](ksetup-delrealmflags.md)
