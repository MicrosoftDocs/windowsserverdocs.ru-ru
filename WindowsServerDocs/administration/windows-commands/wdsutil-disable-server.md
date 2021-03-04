---
title: WDSUTIL Disable — сервер
description: Справочная статья по команде WDSUTIL Disable-Server, которая отключает все службы для сервера служб развертывания Windows.
ms.topic: reference
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 64b5f5006bafe54b5492d78e422420c2d789bea0
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101803937"
---
# <a name="wdsutil-disable-server"></a>WDSUTIL Disable — сервер

Отключает все службы для сервера служб развертывания Windows.

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /Disable-Server [/Server:<Server name>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер. |

## <a name="examples"></a>Примеры

Чтобы отключить сервер, введите:

```
wdsutil /Disable-Server
```

```
wdsutil /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
