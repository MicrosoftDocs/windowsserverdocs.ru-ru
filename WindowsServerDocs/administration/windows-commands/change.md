---
title: Изменить
description: Справочный раздел по команде Change, которая изменяет удаленный рабочий стол параметры сервера узла сеансов для входа в систему, сопоставления COM-портов и режима установки.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a35bd558898b3991a9e6f847d415a67d70f0d01b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82715515"
---
# <a name="change"></a>Изменить

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменения удаленный рабочий стол параметры сервера узла сеансов для входа в систему, сопоставления COM-портов и режима установки.

> [!NOTE]
> В Windows Server 2008 R2 службы терминалов были переименованы на службы удаленных рабочих столов. Чтобы узнать о новых возможностях последней версии, см. статью [новые возможности службы удаленных рабочих столов в Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Синтаксис

 ```
 change logon
 change port
 change user
 ```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| [Команда "изменить вход"](change-logon.md) | Включает или отключает вход из сеансов клиента на удаленный рабочий стол сервере узла сеансов или отображает текущее состояние входа в систему. |
| [Команда "изменить порт"](change-port.md) | Перечисление или изменение сопоставления COM-портов для совместимости с приложениями MS-DOS. |
| [Команда "изменить пользователя"](change-user.md) | Изменяет режим установки для сервера узла сеансов удаленный рабочий стол. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам служб удаленных рабочих столов (служб терминалов)](remote-desktop-services-terminal-services-command-reference.md)
