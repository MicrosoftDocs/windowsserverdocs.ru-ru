---
title: WDSUTIL Remove-Namespace
description: Справочная статья по WDSUTIL Remove-Namespace, которая удаляет пользовательское пространство имен.
ms.topic: reference
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bc5d44b727bf93bf6630f7289833640397e69dae
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731278"
---
# <a name="wdsutil-remove-namespace"></a>WDSUTIL Remove-Namespace

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет пользовательское пространство имен.

## <a name="syntax"></a>Синтаксис
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|Имен<Namespace name>|Указывает имя пространства имен. Это не понятное имя, оно должно быть уникальным.<p>-   **Служба роли сервера развертывания**: синтаксис имени пространства имен —/namespace: WDS: <ImageGroup> / <ImageName> / <Index> . Например: **WDS: ImageGroup1/install. wim/1**<br />-   **Служба роли транспортного сервера**: это значение должно совпадать с именем, присвоенным пространству имен при его создании на сервере.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.|
|/Force|немедленно удаляет пространство имен и завершает работу всех клиентов. Обратите внимание, что если не указать **/Force**, существующие клиенты могут завершить перенос, но новые клиенты не смогут присоединиться.|
## <a name="examples"></a>Примеры
Чтобы присвоить пространство имен (текущие клиенты могут завершить процесс перемещения, но новые клиенты не смогут присоединиться), введите:
```
wdsutil /remove-Namespace /Namespace:Custom Auto 1
```
Для принудительного завершения работы всех клиентов введите:
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /force
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Get-аллнамеспацес](wdsutil-get-allnamespaces.md)
- [Команда WDSUTIL New-Namespace](wdsutil-new-namespace.md)
- [Команда WDSUTIL Start-Namespace](wdsutil-start-namespace.md)
