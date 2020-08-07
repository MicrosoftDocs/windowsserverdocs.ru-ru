---
title: serverweroptin
description: Справочная статья для * * * *-
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9bcedf0d855980b193f466e719483ec268afd40c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882720"
---
# <a name="serverweroptin"></a>serverweroptin

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет включить отчеты об ошибках.
## <a name="syntax"></a>Синтаксис
```
serverweroptin [/query] [/detailed] [/summary]
```
#### <a name="parameters"></a>Параметры
|Параметр|Описание:|
|-------|--------|
|/Query|проверяет текущее значение параметра.|
|/детаилед|Автоматически отправляет подробные отчеты.|
|/Summary|Автоматически отправляет сводные отчеты.|
|/?|Отображение справки в командной строке.|
## <a name="examples"></a>Примеры
Чтобы проверить текущее значение параметра, введите:
```
serverweroptin /query
```
Чтобы автоматически отправить подробные отчеты, введите:
```
serverweroptin /detailed
```
Чтобы автоматически отправить сводные отчеты, введите
```
serverweroptin /summary
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

