---
title: sxstrace
description: Справочная статья по команде систраце, которая помогает диагностировать проблемы, связанные с параллельным управлением.
ms.topic: reference
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: eb73a173caaa13eee2cfeb8bf158089ff774f2bb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805547"
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
