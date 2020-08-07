---
title: Remove-Namespace
description: Справочная статья по Remove-Namespace, которая удаляет пользовательское пространство имен.
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a85552109f85e0c4de5f3d09c9c0335dccc5af1f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891906"
---
# <a name="using-the-remove-namespace-command"></a>Использование команды Remove-Namespace

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
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-allnamespaces-command.md) 
 Get-аллнамеспацес [Использование команды](using-the-new-namespace-command.md) 
 New-Namespace [Подкоманда: Start-Namespace](subcommand-start-namespace.md)
