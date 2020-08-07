---
title: Update-Серверфилес
description: Справочная статья по Update-Серверфилес, которая обновляет файлы в общей папке REMINST с использованием последних файлов, которые хранятся в папке%Windir%\System32\RemInst сервера.
ms.topic: article
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f60e5b5c5208d5718a287fd2d012368d13fad9f9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881467"
---
# <a name="update-serverfiles"></a>Update-Серверфилес

Обновляет файлы в общей папке REMINST с помощью последних файлов, которые хранятся в папке%Windir%\System32\RemInst сервера. Чтобы обеспечить допустимость установки служб развертывания Windows, эту команду следует выполнять один раз после каждого обновления сервера, установки пакета обновления или обновления файлов служб развертывания Windows.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание:|
|---------|-----------|
|[/Server: \<Server name> ]|Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.|

## <a name="examples"></a>Примеры

Чтобы обновить файлы, введите одно из следующих действий.
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)