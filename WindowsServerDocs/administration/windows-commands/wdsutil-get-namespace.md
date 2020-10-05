---
title: WDSUTIL Get — пространство имен
description: Справочная статья по WDSUTIL Get-Namespace, в которой отображаются сведения о пользовательском пространстве имен.
ms.topic: reference
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2c88bd26af900950c33b059822c08f5afb40de77
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730783"
---
# <a name="wdsutil-get-namespace"></a>WDSUTIL Get — пространство имен

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о пользовательском пространстве имен.

## <a name="syntax"></a>Синтаксис
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/Show:Clients]
```
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/details:Clients]
```
### <a name="parameters"></a>Параметры

|               Параметр               |                                                                                                                                                                                         Описание                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      Имен<Namespace name>      | Указывает имя пространства имен. Обратите внимание, что это не понятное имя, оно должно быть уникальным.<p>-Сервер развертывания. синтаксис имени пространства имен —/Намспаце: WDS: <ImageGroup> / <ImageName> / <Index> . Например: **WDS: ImageGroup1/install. wim/1**<br />— Транспортный сервер. это значение должно совпадать с именем, присвоенным пространству имен при его создании на сервере. |
|        [/Server: <Server name> ]        |                                                                                                             Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.                                                                                                              |
| [/Show: Clients] или [/детаилс: Clients] |                                                                                                                                                  Отображает сведения о клиентских компьютерах, подключенных к указанному пространству имен.                                                                                                                                                  |

## <a name="examples"></a>Примеры
Чтобы просмотреть сведения о пространстве имен, введите:
```
wdsutil /Get-Namespace /Namespace:Custom Auto 1
```
Чтобы просмотреть сведения о пространстве имен и подключенных клиентах, введите одно из следующих действий:
- Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /Show:Clients`
- Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /details:Clients`

## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллнамеспацес](wdsutil-get-allnamespaces.md)
- [Команда WDSUTIL New-Namespace](wdsutil-new-namespace.md)
- [Команда WDSUTIL Remove-Namespace](wdsutil-remove-namespace.md)
- [Команда WDSUTIL Start-Namespace](wdsutil-start-namespace.md)
