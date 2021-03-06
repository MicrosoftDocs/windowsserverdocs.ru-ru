---
title: ksetup addrealmflags
description: Справочная статья по команде ksetup аддреалмфлагс, которая добавляет дополнительные флаги сферы в указанную область.
ms.topic: reference
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4abe13c8d38060082717dc17e7a40d7c75a7c984
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101815618"
---
# <a name="ksetup-addrealmflags"></a>ksetup addrealmflags

Добавляет дополнительные флаги сферы в указанную область.

## <a name="syntax"></a>Синтаксис

```
ksetup /addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. |

#### <a name="remarks"></a>Комментарии

- Флаги сферы задают дополнительные возможности области Kerberos, которые не основаны на операционной системе Windows Server. Компьютеры под управлением Windows Server могут использовать сервер Kerberos для администрирования проверки подлинности в области Kerberos вместо использования домена под управлением операционной системы Windows Server. Эта запись устанавливает функции области и имеет следующие значения:

| Значение | Флаг области | Описание |
| ----- | ---------- | ----------- |
| 0xF | Все | Заданы все флаги сферы. |
| 0x00 | None | Флаги области не заданы, а дополнительные функции не включены. |
| 0x01 | сендаддресс | IP-адрес будет включаться в билеты предоставления билетов. |
| 0x02 | ткпсуппортед | В этой области поддерживаются протоколы TCP и UDP (User Datagram Protocol). |
| 0x04 | delegate | Все пользователи в этой области являются доверенными для делегирования. |
| 0x08 | нксуппортед | Эта область поддерживает канонизации имен, что позволяет использовать стандарты именования DNS и областей. |
| 0x80 | RC4 | Эта область поддерживает шифрование RC4 для включения доверительных отношений между сферами, что позволяет использовать TLS. |

- Флаги сферы хранятся в реестре в разделе `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` . Эта запись не существует в реестре по умолчанию. Для заполнения реестра можно использовать команду [ksetup аддреалмфлагс](ksetup-addrealmflags.md) .

- Чтобы увидеть доступные и установленные флаги области, просмотрите выходные данные **ksetup** или `ksetup /dumpstate` .

### <a name="examples"></a>Примеры

Чтобы получить список доступных флагов области для области CONTOSO, введите:

```
ksetup /listrealmflags
```

Чтобы задать два флага для области CONTOSO, введите:

```
ksetup /setrealmflags CONTOSO ncsupported delegate
```

Чтобы добавить еще один флаг, не находящегося в наборе, введите:

```
ksetup /addrealmflags CONTOSO SendAddress
```

Чтобы проверить, установлен ли флаг области, введите `ksetup` и просмотрите выходные данные, выполняя поиск текста, **Флаги области =**. Если текст не отображается, это означает, что флаг не установлен.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup листреалмфлагс, команда](ksetup-listrealmflags.md)

- [ksetup сетреалмфлагс, команда](ksetup-setrealmflags.md)

- [ksetup делреалмфлагс, команда](ksetup-delrealmflags.md)

- [ksetup думпстате, команда](ksetup-dumpstate.md)
