---
title: WDSUTIL Get-Server
description: Справочная статья по WDSUTIL Get-Server, которая получает сведения с указанного сервера служб развертывания Windows.
ms.topic: reference
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9c697ee8823d8f97765f3bed82a887d793e940d5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825751"
---
# <a name="wdsutil-get-server"></a>WDSUTIL Get-Server

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Извлекает сведения с указанного сервера служб развертывания Windows.

## <a name="syntax"></a>Синтаксис
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|[/Server: <Server name> ]|Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер.|
|/Show: {config &#124; Images &#124; ALL}|Указывает тип возвращаемых данных.<p>-   **Config** возвращает сведения о конфигурации.<br />-   **Изображения** возвращают сведения о группах образов, загрузочных образах и образах установки.<br />-   **ALL** возвращает сведения о конфигурации и сведения об образе.|
|[/детаилед]|Этот параметр можно использовать с **/Show: Images** или **/Show: ALL** , чтобы указать, что должны возвращаться все метаданные образа из каждого изображения. Если параметр **/детаилед** не используется, по умолчанию возвращается имя образа, описание и имя файла.|
## <a name="examples"></a>Примеры
Чтобы просмотреть сведения о сервере, введите:
```
wdsutil /Get-Server /Show:Config
```
Чтобы просмотреть подробные сведения о сервере, введите:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL Disable-Server](wdsutil-disable-server.md)
- [Команда WDSUTIL Enable-Server](wdsutil-enable-server.md)
- [WDSUTIL Initialize-Server, команда](wdsutil-initialize-server.md)
- [Команда WDSUTIL Set-Server](wdsutil-set-server.md)
- [Команда WDSUTIL Start-Server](wdsutil-start-server.md)
- [Команда WDSUTIL-сервер](wdsutil-stop-server.md)
- [Команда WDSUTIL Uninitialize-Server](wdsutil-uninitialize-server.md)
