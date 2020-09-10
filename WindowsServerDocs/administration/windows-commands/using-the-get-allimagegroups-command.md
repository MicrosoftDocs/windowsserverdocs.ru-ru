---
title: Get-Аллимажеграупс
description: Справочная статья по Get-Аллимажеграупс, которая извлекает сведения обо всех группах образов на сервере и всех образах в этих группах образов.
ms.topic: reference
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b69375cff867d317c3ac6c83ec1c75358455ac03
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626426"
---
# <a name="get-allimagegroups"></a>Get-Аллимажеграупс

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения обо всех группах образов на сервере и всех образах в этих группах образов.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|
|[/детаилед]|Возвращает метаданные изображения из каждого изображения. Если этот параметр не используется, поведение по умолчанию — возврат только имени, описания и имени файла для каждого образа.|
## <a name="examples"></a>Примеры
Чтобы просмотреть сведения о группах образов, введите одно из следующих действий:
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды](using-the-add-imagegroup-command.md) 
 Add-имажеграуп [Использование команды](using-the-get-imagegroup-command.md) 
 Get-имажеграуп [Использование команды](using-the-remove-imagegroup-command.md) 
 Remove-имажеграуп [Подкоманда: Set-имажеграуп](subcommand-set-imagegroup.md)
