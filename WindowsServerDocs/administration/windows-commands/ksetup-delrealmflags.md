---
title: ksetup delrealmflags
description: Справочная статья по команде ksetup делреалмфлагс, которая удаляет флаги сферы из указанной области.
ms.topic: reference
ms.assetid: 22053041-1eb4-47f5-bed9-3d5681bcde7d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 90ebf697ae19cd31b45dc7744ba29f5dc0b9f597
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640057"
---
# <a name="ksetup-delrealmflags"></a>ksetup delrealmflags

Удаляет флаги сферы из указанной области.

## <a name="syntax"></a>Синтаксис

```
ksetup /delrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM и указывается в качестве области по умолчанию или **области =** при запуске **ksetup** . |

#### <a name="remarks"></a>Примечания

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

- Чтобы увидеть доступные и установленные флаги области, просмотрите выходные данные **ksetup** или `ksetup /dumpstate` .

### <a name="examples"></a>Примеры

Чтобы получить список доступных флагов области для области CONTOSO, введите:

```
ksetup /listrealmflags
```

Чтобы удалить два флага, находящихся в наборе, введите:

```
ksetup /delrealmflags CONTOSO ncsupported delegate
```

Чтобы убедиться, что флаги области были удалены, введите, `ksetup` а затем просмотрите выходные данные, выполняя поиск текста, **Флаги области =**.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup листреалмфлагс, команда](ksetup-listrealmflags.md)

- [ksetup сетреалмфлагс, команда](ksetup-setrealmflags.md)

- [ksetup аддреалмфлагс, команда](ksetup-addrealmflags.md)

- [ksetup думпстате, команда](ksetup-dumpstate.md)
