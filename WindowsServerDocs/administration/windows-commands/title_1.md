---
title: title
description: Справочная статья для Title, которая создает заголовок для окна командной строки.
ms.topic: reference
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1160326d2627b62da120e364941627b64730f721
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640426"
---
# <a name="title"></a>title

Создает заголовок для окна командной строки.



## <a name="syntax"></a>Синтаксис

```
title [<String>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|\<String>|Указывает заголовок окна командной строки.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Примечания

-   Чтобы создать заголовок окна для пакетных программ, включите команду **Title** в начало пакетной программы.
-   После установки заголовка окна его можно сбросить только с помощью команды **Title** .

## <a name="examples"></a>Примеры

В следующем примере скрипта заголовок окна командной строки изменяется на обновление файлов, а пакетный файл выполняет команду **Copy** . После выполнения команды `Files Updated` отображается текст, а название окна командной строки снова меняется на командную строку.
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)