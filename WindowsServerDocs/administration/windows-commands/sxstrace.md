---
title: sxstrace
description: Узнайте, как диагностировать проблемы, связанные с параллельным выполнением.
ms.topic: reference
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7afcb79bf12cf23a66ac564362012c4424e5bbe6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626777"
---
# <a name="sxstrace"></a>sxstrace

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Диагностика проблем с параллельным управлением.

## <a name="syntax"></a>Синтаксис
```
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]
```

#### <a name="parameters"></a>Параметры
|Параметр|Description|
|-------|--------|
|трассировка|Включает трассировку для SxS (параллельно)|
|-файл_журнала|Указывает необработанный файл журнала.|
|\<FileName>|Сохраняет журнал трассировки в файле *filename*.|
|-не останавливаться|Указывает отсутствие запроса на прекращение трассировки.|
|parse|Преобразует необработанный файл трассировки.|
|-файл|Указывает имя выходного файла.|
|\<ParsedFile>|Указывает имя файла проанализированного файла.|
|-filter|Позволяет фильтровать выходные данные.|
|\<AppName>|Указывает имя приложения.|
|стоптраце|Остановите трассировку, если она не была остановлена ранее.|
|-?|Отображение справки в командной строке.|

## <a name="examples"></a>Примеры
Включите трассировку и сохраните файл трассировки в **сксстраце. ETL**:
```
sxstrace trace -logfile:sxstrace.etl
```
Перевести необработанный файл трассировки в удобочитаемый формат и сохранить результат в **sxstrace.txt**:
```
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt
```

## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

