---
title: WDSUTIL Get-имажеграуп
description: Справочная статья по WDSUTIL Get-имажеграуп, которая извлекает сведения о группе образов и изображениях в ней.
ms.topic: reference
ms.assetid: 0fc25aca-a529-44ee-bc8e-96bc8affb458
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e0e90c3640967b4226e75d9d1906bdbb4e806a1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825138"
---
# <a name="wdsutil-get-imagegroup"></a>WDSUTIL Get-имажеграуп

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения о группе образов и содержащихся в ней изображениях.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-ImageGroup ImageGroup:<Image group name> [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|/Имажеграуп:<Image group name>|Указывает имя группы образов.|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|[/детаилед]|Возвращает метаданные изображения для каждого изображения. Если этот параметр не используется, поведение по умолчанию — возврат только имени, описания и имени файла изображения.|
## <a name="examples"></a>Примеры
Чтобы просмотреть сведения о группе образов, введите:
```
wdsutil /Get-ImageGroup ImageGroup:ImageGroup1
```
Чтобы просмотреть сведения, включая метаданные, введите:
```
wdsutil /verbose /Get-ImageGroup ImageGroup:ImageGroup1 /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-имажеграуп](wdsutil-add-imagegroup.md)
- [Команда WDSUTIL Get-аллимажеграупс](wdsutil-get-allimagegroups.md)
- [Команда WDSUTIL Remove-имажеграуп](wdsutil-remove-imagegroup.md)
- [Команда WDSUTIL Set-имажеграуп](wdsutil-set-imagegroup.md)
