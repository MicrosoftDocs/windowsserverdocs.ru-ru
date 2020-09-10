---
title: Get-Device
description: Справочная статья по Get-Device, которая получает сведения о предварительно подготовленном компьютере (т. е. физическом компьютере, который был подключен к учетной записи компьютера в доменных службах Active Directory).
ms.topic: reference
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4fdbdfa843376b328cac0fe06e68a5a215ddd915
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622594"
---
# <a name="get-device"></a>Get-Device

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения о службах развертывания Windows о предварительно подготовленном компьютере (т. е. физическом компьютере, который был подключен к учетной записи компьютера в доменных службах Active Directory).

## <a name="syntax"></a>Синтаксис
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|Модем<Device name>|Указывает имя компьютера (SAMAccountName).|
|Удостоверения<MAC or UUID>|Указывает MAC-адрес или UUID (GUID) компьютера, как показано в следующих примерах. Обратите внимание, что допустимый GUID должен быть в одном из двух форматов двоичная строка или строка GUID<p>-   **Двоичная строка**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **MAC-адрес**: 00B056882FDC (без дефисов) или 00-B0-56-88-2F-DC (с тире)<br />-   **Строка GUID**:/ID: E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6|
|[/Domain: <Domain> ]|Указывает домен для поиска предварительно подготовленного компьютера. Значение этого параметра по умолчанию — локальный домен.|
|[/Forest: {Да &#124; No}]|Указывает, должны ли службы развертывания Windows выполнять поиск по всему лесу или локальному домену. Значение по умолчанию — « **нет**». Это означает, что поиск выполняется только в локальном домене.|
## <a name="examples"></a>Примеры
Чтобы получить сведения, используя имя компьютера, введите:
```
wdsutil /Get-Device /Device:computer1
```
Чтобы получить сведения с помощью MAC-адреса, введите:
```
wdsutil /verbose /Get-Device /ID:00-B0-56-88-2F-DC /Domain:MyDomain
```
Чтобы получить сведения с помощью строки GUID, введите:
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Подкоманда: Set-Device](subcommand-set-device.md) 
 [Использование команды](using-the-add-device-command.md) 
 Add-Device [Использование команды Get-аллдевицес](using-the-get-alldevices-command.md)
