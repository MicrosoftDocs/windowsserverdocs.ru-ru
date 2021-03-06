---
title: telnet send
description: Справочная статья по команде Telnet Send, которая отправляет команды Telnet на сервер Telnet.
ms.topic: reference
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1ba17de31f25df13a800d9b67721bc5cf6771d4f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805187"
---
# <a name="telnet-send"></a>Telnet: send

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отправляет команды Telnet на сервер Telnet.

## <a name="syntax"></a>Синтаксис

```
sen {ao | ayt | brk | esc | ip | synch | <string>} [?]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| AO | Отправляет **выходные данные** команды Telnet Abort. |
| айт | Отправляет команду Telnet **?** |
| брк | Отправляет команду Telnet **БРК**. |
| ESC | Отправляет текущий escape-символ Telnet. |
| см | Отправляет **процесс прерывания** команды Telnet. |
| Синхронизация | Отправка команды Telnet Synch. |
| `<string>` | Отправляет любую строку, введенную на сервер Telnet. |
| ? | Отображает справку, связанную с этой командой. |

## <a name="example"></a>Пример

Чтобы отправить на сервер Telnet **?** команду, введите:

```
sen ayt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
