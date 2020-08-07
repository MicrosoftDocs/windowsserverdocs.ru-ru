---
title: Добавление устройства
description: Справочная статья по надстройке Add-Device, которая предварительно наследует компьютер в доменных службах Active Directory. Предварительно подготовленные компьютеры также называются известными компьютерами.
ms.topic: article
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d23e5a2bc69b782e635fa9a47158274796715edf
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87897012"
---
# <a name="add-device"></a>Добавление устройства

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Предварительная настройка компьютера в доменных службах Active Directory. Предварительно подготовленные компьютеры также называются известными компьютерами. Это позволяет настроить свойства для управления установкой клиента. Например, можно настроить программу сетевой загрузки и файл автоматической установки, который должен получить клиент, а также сервер, с которого клиент должен загрузить программу сетевой загрузки.

## <a name="syntax"></a>Синтаксис
```
wdsutil /add-Device /Device:<Device name> /ID:<UUID | MAC address> [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>]
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/OU:<DN of OU>] [/Domain:<Domain>]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|Модем<computer name>|Указывает имя добавляемого компьютера.|
|/ID: <UUID &#124; MAC-адрес>|Указывает идентификатор GUID/UUID или MAC-адрес компьютера. GUID/UUID должны быть в одном из двух форматов: двоичная строка или строка GUID. Пример:<p>Двоичная строка: **/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6**<p>Строка GUID: **/ID: E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<p>MAC-адрес должен иметь следующий формат: **00B056882FDC** (без дефисов) или **00-B0-56-88-2F-DC** (с тире)|
|[/Реферралсервер: <Server name> ]|Указывает имя сервера, к которому нужно подключиться для загрузки программы сетевой загрузки и загрузочного образа с помощью тривиальных протокол FTP (TFTP).|
|[/Бутпрограм: <Relative path> ]|Указывает относительный путь от папки remoteInstall к программе сетевой загрузки, которую должен получить этот компьютер. Например: boot\x86\pxeboot.com|
|[/Вдсклиентунаттенд: <Relative path> ]|Указывает относительный путь от папки remoteInstall к файлу автоматической установки, который автоматизирует экраны установки клиента служб развертывания Windows.|
|[/User: <домен \ пользователь &#124; User@Domain>]|Задает разрешения для объекта учетной записи компьютера, чтобы предоставить указанному пользователю необходимые права для приподключения компьютера к домену.|
|[/Жоинригхтс: {Жоинонли &#124; Full}]|Указывает тип прав, назначаемых пользователю.<p>-   **Жоинонли** требует от администратора сброса учетной записи компьютера, прежде чем пользователь сможет присоединить компьютер к домену.<br />-   **Full** предоставляет полный доступ пользователю, который включает в себя право присоединить компьютер к домену.|
|[/Жоиндомаин: {Yes &#124; No}]|Указывает, должен ли компьютер быть присоединен к домену как учетная запись компьютера во время установки операционной системы. Значение по умолчанию — **Да**.|
|[/Бутимажепас: <Relative path> ]|Указывает относительный путь от папки remoteInstall к загрузочному образу, который должен использоваться этим компьютером.|
|[/OU: <DN of OU> ]|Различающееся имя подразделения, в котором должен быть создан объект учетной записи компьютера. Например: **OU = MyOU, CN = test, DC = Domain, DC = com**. Расположение по умолчанию — это контейнер компьютера по умолчанию.|
|[/Domain: <Domain> ]|Домен, в котором должен быть создан объект учетной записи компьютера. Расположение по умолчанию — локальный домен.|
## <a name="examples"></a>Примеры
Чтобы добавить компьютер с помощью MAC-адреса, введите:
```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```
Чтобы добавить компьютер с помощью строки GUID, введите:
```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com
/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:OU=MyOU,CN=Test,DC=Domain,DC=com
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-get-alldevices-command.md) 
 Get-аллдевицес [Использование команды](using-the-get-device-command.md) 
 Get-Device [Подкоманда: Set-Device](subcommand-set-device.md) 
 [New-WdsClient](/previous-versions/windows/powershell-scripting/dn283430(v=wps.630))
