---
title: WDSUTIL Initialize-Server
description: Справочная статья по WDSUTIL Initialize-Server, которая настраивает сервер служб развертывания Windows для первоначального использования после установки роли сервера.
ms.topic: reference
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 42d579b7139f7ff516d9ff239c535ecd2be42474
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730767"
---
# <a name="wdsutil-initialize-server"></a>WDSUTIL Initialize-Server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Настраивает сервер служб развертывания Windows для первоначального использования после установки роли сервера. После выполнения этой команды следует использовать команду [вдсутиладд-Image](wdsutil-add-image.md) , чтобы добавить образы на сервер.
## <a name="syntax"></a>Синтаксис
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Реминст:<Full path>|Указывает полный путь и имя папки remoteInstall. Если указанная папка еще не существует, этот параметр будет создан при выполнении команды. Всегда следует вводить локальный путь даже в случае удаленного компьютера. Например: **д:\ремотеинсталл**.|
|/Authorize|Авторизация сервера в протоколе DHCP. Этот параметр необходим только в том случае, если включено обнаружение мошеннических DHCP-серверов, что означает, что сервер PXE служб развертывания Windows должен быть авторизован в службе DHCP перед обслуживанием клиентских компьютеров. Обратите внимание, что обнаружение случайного DHCP-сервера отключено по умолчанию.|
## <a name="examples"></a>Примеры
Чтобы инициализировать сервер и установить общую папку remoteInstall на диск F:, введите.
```
wdsutil /Initialize-Server /remInst:F:\remoteInstall
```
Чтобы инициализировать сервер и задать для общей папки remoteInstall диск C:, введите.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:C:\remoteInstall
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-Server](wdsutil-disable-server.md)
- [Команда WDSUTIL Enable-Server](wdsutil-enable-server.md)
- [Команда WDSUTIL Get-Server](wdsutil-get-server.md)
- [Команда WDSUTIL Set-Server](wdsutil-set-server.md)
- [Команда WDSUTIL Start-Server](wdsutil-start-server.md)
- [Команда WDSUTIL-сервер](wdsutil-stop-server.md)
- [Команда WDSUTIL Uninitialize-Server](wdsutil-uninitialize-server.md)
