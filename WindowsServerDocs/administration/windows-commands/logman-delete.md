---
title: logman delete
description: Справочная статья по команде Logman DELETE, которая удаляет существующий сборщик данных.
ms.topic: reference
ms.assetid: 8f3b2422-3dce-4fb4-adbb-8536b1d7da2b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 57d909a23e65de3c74daff4fe82f42943cb3875d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634370"
---
# <a name="logman-delete"></a>logman delete

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет существующий сборщик данных.

## <a name="syntax"></a>Синтаксис

```
logman delete <[-n] <name>> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -s `<computer name>` | Выполняет команду на указанном удаленном компьютере. |
| -config `<value>` | Указывает файл параметров, содержащий параметры команды. |
| [-n] `<name>` | Имя целевого объекта. |
| -ETS | Отправляет команды в сеансы трассировки событий напрямую без сохранения или планирования. |
| -[-] u `<user [password]>` | Указывает пользователя для запуска от имени. При вводе \* для пароля выводится запрос на ввод пароля. Пароль не отображается при вводе. |
| /? | Отображает контекстную справку. |

### <a name="examples"></a>Примеры

Чтобы удалить *perf_log*сборщика данных, введите:

```
logman delete perf_log
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда logman](logman.md)
