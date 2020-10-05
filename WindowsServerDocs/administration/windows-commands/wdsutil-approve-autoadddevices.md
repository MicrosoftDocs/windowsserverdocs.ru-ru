---
title: WDSUTIL утвердить — аутоадддевицес
description: Справочная статья по WDSUTIL утвердить-аутоадддевицес, которая утверждает компьютеры, ожидающие административного утверждения.
ms.topic: reference
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 30074d7b92898e579bbd0cc8f963fc3d8b56c59a
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731028"
---
# <a name="wdsutil-approve-autoadddevices"></a>WDSUTIL утвердить — аутоадддевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Утверждает компьютеры, ожидающие административного утверждения. Если включена политика автоматического добавления, то перед неизвестными компьютерами (не требующими предварительной подготовки) требуется административное утверждение, чтобы установить образ. Эту политику можно включить с помощью вкладки **Отклик PXE** страницы свойств сервера.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>]
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|/Рекуестид: {идентификатор запроса &#124; все}|Указывает идентификатор запроса, назначенный ожидающему компьютеру. Укажите **все** , чтобы утвердить все ожидающие компьютеры.|
|[/Мачиненаме: <Device name> ]|Указывает имя добавляемого компьютера. Этот параметр нельзя использовать при утверждении всех компьютеров.|
|[/OU: <DN of OU> ]|Определяет различающееся имя подразделения, в котором должен быть создан объект учетной записи компьютера. Например: **OU = MyOU, CN = test, DC = Domain, DC = com**. Расположение по умолчанию — это контейнер компьютера по умолчанию.|
|[/User: <домен \ пользователь &#124; User@Domain>]|Задает разрешения для объекта учетной записи компьютера, чтобы назначить указанного пользователя необходимые права.|
|[/Жоинригхтс: {Жоинонли &#124; Full}]|Указывает тип прав, назначаемых указанному пользователю.<p>-   **Жоинонли** требует от администратора сброса учетной записи компьютера, прежде чем пользователь сможет присоединить компьютер к домену.<br />-   **Full** предоставляет полный доступ пользователю, который включает в себя право присоединить компьютер к домену.|
|[/Жоиндомаин: {Yes &#124; No}]|Указывает, должен ли компьютер быть присоединен к домену как учетная запись компьютера во время установки операционной системы. Значение по умолчанию — **Да**.|
|[/Реферралсервер: <Server name> ]|Указывает имя сервера, к которому нужно подключиться для загрузки программы сетевой загрузки и загрузочного образа с помощью тривиальных протокол FTP (TFTP).|
|[/Бутпрограм: <Relative path> ]|Указывает относительный путь от папки remoteInstall к программе сетевой загрузки, которую должен получить этот компьютер. Например: **boot\x86\pxeboot.com**.|
|[/Вдсклиентунаттенд: <Relative path> ]|Указывает относительный путь от папки remoteInstall к файлу автоматической установки, который автоматизирует клиент служб развертывания Windows.|
|[/Бутимажепас: <Relative path> ]|Указывает относительный путь от папки remoteInstall к загрузочному образу, который должен быть получен этим компьютером.|
## <a name="examples"></a>Примеры
Чтобы утвердить компьютер с кодом запроса 12, введите:
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
Чтобы утвердить компьютер с ИД запроса 20 и развернуть образ с указанными параметрами, введите:
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:OU=Test,CN=company,DC=Domain,DC=Com /User:Domain\User1
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
Чтобы утвердить все ожидающие компьютеры, введите:
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Delete-аутоадддевицес](wdsutil-delete-autoadddevices.md)
- [Команда WDSUTIL Get-аутоадддевицес](wdsutil-get-autoadddevices.md)
- [Команда WDSUTIL Reject-аутоадддевицес](wdsutil-reject-autoadddevices.md)
