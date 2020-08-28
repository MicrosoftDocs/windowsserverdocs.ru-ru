---
title: serverweroptin
description: Справочная статья для * * * *-
ms.topic: reference
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f7cb7608df0303cdbd119862cf1349f89c37d13
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037412"
---
# <a name="serverweroptin"></a>serverweroptin

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет включить отчеты об ошибках.
## <a name="syntax"></a>Синтаксис
```
serverweroptin [/query] [/detailed] [/summary]
```
#### <a name="parameters"></a>Параметры
|Параметр|Описание|
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

