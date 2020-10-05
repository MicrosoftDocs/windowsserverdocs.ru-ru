---
title: sxstrace
description: Справочная статья по команде систраце, которая помогает диагностировать проблемы, связанные с параллельным управлением.
ms.topic: reference
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 95f52993db56e61b3a1cd4d26a0ef36626421a15
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718211"
---
# <a name="sxstrace"></a>sxstrace

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Диагностика проблем с параллельным управлением.

## <a name="syntax"></a>Синтаксис

```
sxstrace [{[trace -logfile:<filename> [-nostop]|[parse -logfile:<filename> -outfile:<parsedfile>  [-filter:<appname>]}]
```

### <a name="parameters"></a>Параметры

| Параметр | Description |
|--|--|
| трассировка | Включает трассировку параллельно. |
| -файл_журнала | Указывает необработанный файл журнала. |
| `<filename>` | Сохраняет журнал трассировки в `<filename` . |
| -не останавливаться | Указывает, что не следует подавать запрос на завершение трассировки. |
| parse | Преобразует необработанный файл трассировки. |
| -файл | Указывает имя выходного файла. |
| `<parsedfile>` | Указывает имя файла проанализированного файла. |
| -filter | Позволяет фильтровать выходные данные. |
| `<appname>` | Указывает имя приложения. |
| стоптраце | Останавливает трассировку, если она не была остановлена ранее. |
| -? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы включить трассировку и сохранить файл трассировки в *сксстраце. ETL*, введите:

```
sxstrace trace -logfile:sxstrace.etl
```

Чтобы преобразовать необработанный файл трассировки в удобочитаемый формат и сохранить результат в *sxstrace.txt*, введите:

```
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
