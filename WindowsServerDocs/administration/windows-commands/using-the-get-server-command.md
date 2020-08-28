---
title: Get-Server
description: Справочная статья по Get-Server, которая получает сведения с указанного сервера служб развертывания Windows.
ms.topic: reference
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13bceebfb619fc93cbab7b2b45d3dd34838760ed
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029502"
---
# <a name="get-server"></a>Get-Server

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
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Использование команды «Disable-Server»](using-the-disable-server-command.md) 
 [Использование команды](using-the-enable-server-command.md) 
 Enable-Server [Использование команды](using-the-initialize-server-command.md) 
 Initialize-Server [Подкоманда: Set-Server](subcommand-set-server.md) 
 [Подкоманда: Start-Server](subcommand-start-server.md) 
 [Подкоманда:-сервер](subcommand-stop-server.md) 
 [Параметр Uninitialize-Server](the-uninitialize-server-option.md)
