---
title: Программа Logman Import и Logman Export
description: Справочный раздел по программе Logman Import и Logman Export, который импортирует набор сборщиков данных из XML-файла или экспортирует набор сборщиков данных в XML-файл.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44a659abc9e364bf10487e93a7937c1cf8d51bbc
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820574"
---
# <a name="logman-import-and-logman-export"></a>Программа Logman Import и Logman Export

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Импортирует набор сборщиков данных из XML-файла или экспортирует набор сборщиков данных в XML-файл.

## <a name="syntax"></a>Синтаксис

```
logman import <[-n] <name>> <-xml <name>> [options]
logman export <[-n] <name>> <-xml <name>> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -s`<computer name>` | Выполните команду на указанном удаленном компьютере. |
| -config`<value>` | Указывает файл параметров, содержащий параметры команды. |
| [-n]`<name>` | Имя целевого объекта. |
| -XML`<name>` | Имя XML-файла для импорта или экспорта. |
| -ETS | Отправляет команды в сеансы трассировки событий напрямую без сохранения или планирования. |
| -[-] u`<user [password]>` | Указывает пользователя для запуска от имени. При вводе `*` для пароля выводится запрос на ввод пароля. Пароль не отображается при вводе. |
| -y | Отвечает Да на все вопросы без запроса. |
| /? | Отображает контекстную справку. |

### <a name="examples"></a>Примеры

Чтобы импортировать XML-файл *к:\виндовс\ perf_log. XML* с компьютера *server_1* как набор сборщиков данных с именем *perf_log*, введите:

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [logman](logman.md)
