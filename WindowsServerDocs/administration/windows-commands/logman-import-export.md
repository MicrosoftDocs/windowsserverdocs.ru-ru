---
title: logman import and logman export
description: Справочная статья по программе Logman Import и Logman Export, которая импортирует набор сборщиков данных из XML-файла или экспортирует набор сборщиков данных в XML-файл.
ms.topic: reference
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c2da747014f4b5d8c0db5427211d93de59f2c0c4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101813749"
---
# <a name="logman-import-and-logman-export"></a>logman import and logman export

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Импортирует набор сборщиков данных из XML-файла или экспортирует набор сборщиков данных в XML-файл.

## <a name="syntax"></a>Синтаксис

```
logman import <[-n] <name> <-xml <name> [options]
logman export <[-n] <name> <-xml <name> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -s `<computer name>` | Выполните команду на указанном удаленном компьютере. |
| -config `<value>` | Указывает файл параметров, содержащий параметры команды. |
| [-n] `<name>` | Имя целевого объекта. |
| -XML `<name>` | Имя XML-файла для импорта или экспорта. |
| -ETS | Отправляет команды в сеансы трассировки событий напрямую без сохранения или планирования. |
| -[-] u `<user [password]>` | Указывает пользователя для запуска от имени. При вводе `*` для пароля выводится запрос на ввод пароля. Пароль не отображается при вводе. |
| -y | Отвечает Да на все вопросы без запроса. |
| /? | Отображает контекстную справку. |

### <a name="examples"></a>Примеры

Чтобы импортировать XML-файл *c:\windows\perf_log.xml* с компьютера *server_1* как набор сборщиков данных с именем *perf_log*, введите:

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда logman](logman.md)
