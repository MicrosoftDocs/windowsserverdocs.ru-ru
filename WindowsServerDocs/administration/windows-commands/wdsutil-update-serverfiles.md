---
title: Update-ServerFiles
description: Справочная статья по Update-Серверфилес, которая обновляет файлы в общей папке REMINST с использованием последних файлов, которые хранятся в папке%Windir%\System32\RemInst сервера.
ms.topic: reference
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7684dfb694ac6814d00c91363d6573be5cf7be7f
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524899"
---
# <a name="update-serverfiles"></a>Update-ServerFiles

Обновляет файлы в общей папке REMINST с помощью последних файлов, которые хранятся в папке%Windir%\System32\RemInst сервера. Чтобы обеспечить допустимость установки служб развертывания Windows, эту команду следует выполнять один раз после каждого обновления сервера, установки пакета обновления или обновления файлов служб развертывания Windows.

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|

## <a name="examples"></a>Примеры

Чтобы обновить файлы, введите одно из следующих действий.
```
wdsutil /Update-ServerFiles
wdsutil /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)