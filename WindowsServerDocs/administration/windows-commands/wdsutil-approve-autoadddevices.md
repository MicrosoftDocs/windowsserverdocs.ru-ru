---
title: WDSUTIL утвердить — аутоадддевицес
description: Справочная статья по команде WDSUTIL reаутоадддевицес, которая утверждает компьютеры, ожидающие административного утверждения.
ms.topic: reference
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 95261a9897cba9252b92336a656d878dcd6c42ba
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804027"
---
# <a name="wdsutil-approve-autoadddevices"></a>WDSUTIL утвердить — аутоадддевицес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Утверждает компьютеры, ожидающие административного утверждения. Если включена политика автоматического добавления, то перед неизвестными компьютерами (которые не являются предварительно подготовленными) необходимо выполнить административное утверждение, чтобы установить образ. Эту политику можно включить с помощью вкладки **Отклик PXE** страницы свойств сервера.

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Сервером`<Servername>` | Указывает имя сервера. Это может быть NetBIOS-имя или FQDN. Если имя сервера не указано, используется локальный сервер. |
| RequestId`{Request ID|ALL}` | Указывает идентификатор запроса, назначенный ожидающему компьютеру. Укажите **все** , чтобы утвердить все ожидающие компьютеры. |
| ИмяКомпьютера`<Devicename>` | Указывает имя добавляемого устройства. Этот параметр нельзя использовать при утверждении всех компьютеров. |
| [/OU: `<DN of OU>` ] | Различающееся имя подразделения, в котором должен быть создан объект учетной записи компьютера. Например: **OU = MyOU, CN = test, DC = Domain, DC = com**. Расположение по умолчанию — это контейнер компьютера по умолчанию. |
| [/User: `<Domain\User|User@Domain>` ] | Задает разрешения для объекта учетной записи компьютера, чтобы предоставить указанному пользователю необходимые права для приподключения компьютера к домену. |
| [/Жоинригхтс: `{JoinOnly|Full}` ] | Указывает тип прав, назначаемых пользователю.<ul><li>**Жоинонли** — требует от администратора сброса учетной записи компьютера, прежде чем пользователь сможет присоединить компьютер к домену.</li><li>**Full** — предоставляет полный доступ пользователю, который включает в себя право присоединить компьютер к домену. |
| [/Жоиндомаин: `{Yes|No}` ] | Указывает, должен ли компьютер быть присоединен к домену как учетная запись компьютера в процессе установки операционной системы. Значение по умолчанию — **Да**. |
| [/Реферралсервер: `<Servername>` ] | Указывает имя сервера для связи, чтобы загрузить программу сетевой загрузки и загрузочный образ с помощью тривиальных протокол FTP (TFTP). |
| [/Бутпрограм: `<Relativepath>` ] | Указывает относительный путь от папки **remoteInstall** к программе сетевой загрузки, которую должен получить этот компьютер. Например: **boot\x86\pxeboot.com**. |
| [/Вдсклиентунаттенд: `<Relativepath>` ] | Указывает относительный путь от папки **remoteInstall** к файлу автоматической установки, который автоматизирует клиент служб развертывания Windows. |
| [/Бутимажепас: `<Relativepath>` ] | Указывает относительный путь от папки remoteInstall к загрузочному образу, который должен быть получен этим компьютером. |

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

- [Командлеты служб развертывания Windows](/powershell/module/wds)
