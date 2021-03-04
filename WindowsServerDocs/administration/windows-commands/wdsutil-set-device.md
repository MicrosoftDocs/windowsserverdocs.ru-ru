---
title: WDSUTIL Set-Device
description: Справочная статья по WDSUTIL Set-Device, в котором изменяются атрибуты предварительно подготовленного компьютера.
ms.topic: reference
ms.assetid: 401567f8-eaeb-4a2d-b811-140bb007028d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 131d8de0255b55b7c35ecc7323bdae83251ecf3d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826353"
---
# <a name="wdsutil-set-device"></a>WDSUTIL Set-Device

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет атрибуты предварительно подготовленного компьютера. Предварительно подготовленный компьютер — это компьютер, который был связан с объектом учетной записи компьютера на серверах домена Active Directory (AD DS). Предварительно подготовленные клиенты также называются известными компьютерами. Для управления установкой клиента можно настроить свойства учетной записи компьютера. Например, можно настроить программу сетевой загрузки и файл автоматической установки, который должен получить клиент, а также сервер, с которого клиент должен загрузить программу сетевой загрузки.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Set-Device /Device:<Device name> [/ID:<UUID | MAC address>] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>]
[/WdsClientUnattend:<Relative path>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/Domain:<Domain>] [/resetAccount]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|Модем<computer name>|Указывает имя компьютера (SAM-Account-Name).|
|[/ID: <UUID &#124; MAC-адрес>]|Указывает идентификатор GUID/UUID или MAC-адрес компьютера. Это значение должно быть в одном из следующих трех форматов:<p>-Двоичная строка: **/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6**<br />-GUID/UUID строка:/ID:**E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br />— MAC-адрес: **00B056882FDC** (без дефисов) или **00-B0-56-88-2F-DC** (с тире)|
|[/Реферралсервер: <Server name> ]|Указывает имя сервера для связи, чтобы загрузить программу сетевой загрузки и загрузочный образ с помощью тривиальных протокол FTP (TFTP).|
|[/Бутпрограм: <Relative path> ]|Указывает относительный путь от папки remoteInstall к программе сетевой загрузки, которую будет получить указанный компьютер. Например: **boot\x86\pxeboot.com**|
|[/Вдсклиентунаттенд: <Relative path> ]|Указывает относительный путь от папки remoteInstall к файлу Unattend, который автоматизирует экраны установки для клиента служб развертывания Windows.|
|[/User: <домен \ пользователь &#124; User@Domain>]|Задает разрешения для объекта учетной записи компьютера, чтобы предоставить указанному пользователю необходимые права для приподключения компьютера к домену.|
|[/Жоинригхтс: {Жоинонли &#124; Full}]|Указывает тип прав, назначаемых пользователю.<p>-   **Жоинонли** требует от администратора сброса учетной записи компьютера, прежде чем пользователь сможет присоединить компьютер к домену.<br />-   **Full** предоставляет полный доступ пользователю, включая право присоединить компьютер к домену.|
|[/Жоиндомаин: {Yes &#124; No}]|Указывает, должен ли компьютер быть присоединен к домену как учетная запись компьютера в ходе установки служб развертывания Windows. Значение по умолчанию — **Да**.|
|[/Бутимажепас: <Relative path> ]|Указывает относительный путь от папки remoteInstall к загрузочному образу, который будет использоваться компьютером.|
|[/Domain: <Domain> ]|Указывает домен для поиска предварительно подготовленного компьютера. Значение по умолчанию — локальный домен.|
|[/Ресетаккаунт]|Сбрасывает разрешения на указанном компьютере, чтобы любой пользователь с соответствующими разрешениями мог присоединиться к домену с помощью этой учетной записи.|
## <a name="examples"></a>Примеры
Чтобы задать программу сетевой загрузки и сервер ссылок для компьютера, введите:
```
wdsutil /Set-Device /Device:computer1 /ReferralServer:MyWDSServer
/BootProgram:boot\x86\pxeboot.n12
```
Чтобы задать различные параметры для компьютера, введите:
```
wdsutil /verbose /Set-Device /Device:computer2 /ID:00-B0-56-88-2F-DC /WdsClientUnattend:WDSClientUnattend\unattend.xml
/User:Domain\user /JoinRights:JoinOnly /JoinDomain:No /BootImagepath:boot\x86\images\boot.wim /Domain:NorthAmerica /resetAccount
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-Device](wdsutil-add-device.md)
- [Команда WDSUTIL Get-аллдевицес](wdsutil-get-alldevices.md)
- [Команда WDSUTIL Get-Device](wdsutil-get-device.md)
