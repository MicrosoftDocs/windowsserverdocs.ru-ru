---
title: WDSUTIL Start — пространство имен
description: Справочная статья для подкоманды Start-Namespace, которая запускает Scheduled-Cast пространство имен.
ms.topic: reference
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a11f0309e5299a26e80b786a6fe10dd849ec4dea
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826203"
---
# <a name="wdsutil-start-namespace"></a>WDSUTIL Start — пространство имен

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает Scheduled-Cast пространство имен.

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
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллнамеспацес](wdsutil-get-allnamespaces.md)
- [Команда WDSUTIL New-Namespace](wdsutil-new-namespace.md)
- [Команда WDSUTIL Remove-Namespace](wdsutil-remove-namespace.md)
