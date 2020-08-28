---
title: sxstrace
description: Узнайте, как диагностировать проблемы, связанные с параллельным выполнением.
ms.topic: reference
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a5398a9dcab96719de998a86bfa74df67a3f39b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024598"
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

