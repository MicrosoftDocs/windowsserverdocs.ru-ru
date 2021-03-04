---
title: telnet unset
description: Справочная статья по команде Telnet Set, которая отключает ранее установленные параметры.
ms.topic: reference
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c10b497dd6321692ae5935a218d728ccd6e7b377
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805127"
---
# <a name="telnet-unset"></a>Telnet: не задано

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отключает ранее установленные параметры.

## <a name="syntax"></a>Синтаксис

```
u {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| бсасдел | Отправляет **Backspace** в виде **Backspace**. |
| CRLF | Отправляет клавишу **Ввод** в виде CR. Также называется режимом перевода строки. |
| деласбс | Отправляет **Удаление** как **Удаление**. |
| escape-знак | Удаляет параметр escape-символа. |
| локалечо | Отключает локалечо. |
| Ведение журнала | Отключает ведение журнала. |
| NTLM | Отключает проверку подлинности NTLM. |
| ? | Отображает справку для этой команды. |

## <a name="example"></a>Пример

Отключите ведение журнала.

```
u logging
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
