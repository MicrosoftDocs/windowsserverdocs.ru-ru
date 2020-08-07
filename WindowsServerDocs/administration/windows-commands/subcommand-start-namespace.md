---
title: Подкоманда Start — пространство имен
description: Справочная статья для подкоманды Start-Namespace, которая запускает пространство имен, запланированное для приведения.
ms.topic: article
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a80664fb4a4f90f58823b87f278b344561422ef
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882082"
---
# <a name="subcommand-start-namespace"></a>Подкоманда: Start-Namespace

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает пространство имен, запланированное для приведения.

## <a name="syntax"></a>Синтаксис
```
wdsutil /start-Namespace /Namespace:<Namespace name[/Server:<Server name>]
```
### <a name="parameters"></a>Параметры

|          Параметр          |                                                                                                                                                                                             Описание                                                                                                                                                                                             |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Namespace: <имя пространства имен| Указывает имя пространства имен. Обратите внимание, что это не понятное имя, оно должно быть уникальным.<p>-   **Сервер развертывания**. синтаксис имени пространства имен —/НАМСПАЦЕ: WDS: <Image group> / <Image name> / <Index> . Например: **WDS: ImageGroup1/install. wim/1**<br />-   **Транспортный сервер**. это имя должно совпадать с именем, присвоенным пространству имен при его создании на сервере. |
|   [/Server: <Server name> ]   |                                                                                                           Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.                                                                                                           |

## <a name="examples"></a>Примеры
Чтобы запустить пространство имен, введите одно из следующих действий:
```
wdsutil /start-Namespace /Namespace:Custom Auto 1
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-allnamespaces-command.md) 
 Get-аллнамеспацес [Использование команды](using-the-new-namespace-command.md) 
 New-Namespace [Использование команды Remove-Namespace](using-the-remove-namespace-command.md)
