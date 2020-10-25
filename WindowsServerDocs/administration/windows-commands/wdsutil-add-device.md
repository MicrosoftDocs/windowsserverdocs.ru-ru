---
title: WDSUTIL Add-Device
description: Справочная статья по команде WDSUTIL Add-Device, которая предварительно размещает компьютер в домен Active Directory Services.
ms.topic: reference
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: de05d5510e61f5cba0813a7e11215935fd380968
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524640"
---
# <a name="wdsutil-add-device"></a>WDSUTIL Add-Device

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Предварительно разэтапный компьютер в домен Active Directory Services (AD DS). Предварительно подготовленные компьютеры также называются *известными компьютерами*. Это позволяет настроить свойства для управления установкой клиента. Например, можно настроить программу сетевой загрузки и файл автоматической установки, который должен получить клиент, а также сервер, с которого клиент должен загрузить программу сетевой загрузки.

## <a name="syntax"></a>Синтаксис

```
wdsutil /add-Device /Device:<Devicename> /ID:<UUID | MAC address> [/ReferralServer:<Servername>] [/BootProgram:<Relativepath>] [/WdsClientUnattend:<Relativepath>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relativepath>] [/OU:<DN of OU>] [/Domain:<Domain>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Модем`<Devicename>` | Указывает имя добавляемого устройства. |
| Удостоверения`<UUID|MAC address>` | Указывает идентификатор GUID/UUID или MAC-адрес компьютера. GUID/UUID должны иметь один из двух форматов: двоичная строка ( `/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6` ) или строка GUID ( `/ID:E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6` ). MAC-адрес должен иметь следующий формат: **00B056882FDC** (без дефисов) или **00-B0-56-88-2F-DC** (с тире) |
| [/Реферралсервер: `<Servername>` ] | Указывает имя сервера, к которому нужно подключиться для загрузки программы сетевой загрузки и загрузочного образа с помощью тривиальных протокол FTP (TFTP). |
| [/Бутпрограм: `<Relativepath>` ] | Указывает относительный путь от папки **remoteInstall** к программе сетевой загрузки, которую должен получить этот компьютер. Пример: `boot\x86\pxeboot.com` |
| [/Вдсклиентунаттенд: `<Relativepath>` ] | Указывает относительный путь от папки **remoteInstall** к файлу автоматической установки, который автоматизирует экраны установки клиента служб развертывания Windows. |
| [/User: `<Domain\User|User@Domain>` ] | Задает разрешения для объекта учетной записи компьютера, чтобы предоставить указанному пользователю необходимые права для приподключения компьютера к домену. |
| [/Жоинригхтс: `{JoinOnly|Full}` ] | Указывает тип прав, назначаемых пользователю.<ul><li>**Жоинонли** — требует от администратора сброса учетной записи компьютера, прежде чем пользователь сможет присоединить компьютер к домену.</li><li>**Full** — предоставляет полный доступ пользователю, который включает в себя право присоединить компьютер к домену. |
| [/Жоиндомаин: `{Yes|No}` ] | Указывает, должен ли компьютер быть присоединен к домену как учетная запись компьютера в процессе установки операционной системы. Значение по умолчанию — **Да**. |
| [/Бутимажепас: `<Relativepath>` ] | Указывает относительный путь от папки **remoteInstall** к загрузочному образу, который должен использоваться этим компьютером. |
| [/OU: `<DN of OU>` ] | Различающееся имя подразделения, в котором должен быть создан объект учетной записи компьютера. Например: **OU = MyOU, CN = test, DC = Domain, DC = com**. Расположение по умолчанию — это контейнер компьютера по умолчанию. |
| [/Domain: `<Domain>` ] | Домен, в котором должен быть создан объект учетной записи компьютера. Расположение по умолчанию — локальный домен. |

## <a name="examples"></a>Примеры

Чтобы добавить компьютер с помощью MAC-адреса, введите:

```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```

Чтобы добавить компьютер с помощью строки GUID, введите:

```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:OU=MyOU,CN=Test,DC=Domain,DC=com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Get-аллдевицес](wdsutil-get-alldevices.md)

- [Команда WDSUTIL Get-Device](wdsutil-get-device.md)

- [Команда WDSUTIL Set-Device](wdsutil-set-device.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)

- [New-WdsClient](/powershell/module/wds/New-WdsClient)
