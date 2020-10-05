---
title: WDSUTIL Get-аллимажеграупс
description: Справочная статья по WDSUTIL Get-аллимажеграупс, которая извлекает сведения обо всех группах образов на сервере и всех образах в этих группах образов.
ms.topic: reference
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 894c9ede958b4583c03d4b0e3b5ac4cca1f39395
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730895"
---
# <a name="wdsutil-get-allimagegroups"></a>WDSUTIL Get-аллимажеграупс

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
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Add-имажеграуп](wdsutil-add-imagegroup.md)
- [Команда WDSUTIL Get-имажеграуп](wdsutil-get-imagegroup.md)
- [Команда WDSUTIL Remove-имажеграуп](wdsutil-remove-imagegroup.md)
- [Команда WDSUTIL Set-имажеграуп](wdsutil-set-imagegroup.md)
