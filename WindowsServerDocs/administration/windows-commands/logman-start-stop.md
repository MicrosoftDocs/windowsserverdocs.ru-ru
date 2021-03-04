---
title: logman start and logman stop
description: Справочная статья по командам Logman Start и Logman Stop, которая запускает сборщик данных и устанавливает время начала вручную или останавливает группу сборщиков данных и устанавливает для времени окончания значение вручную.
ms.topic: reference
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fc887ca5a79910a0af664cc3a6ee7018c158fa76
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101813635"
---
# <a name="logman-start-and-logman-stop"></a>logman start and logman stop

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Команда **Logman Start** запускает сборщик данных и устанавливает время начала вручную. Команда **Logman Stop** останавливает группу сборщиков данных и устанавливает время окончания вручную.

## <a name="syntax"></a>Синтаксис

```
logman start <[-n] <name>> [options]
logman stop <[-n] <name>> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -s `<computer name>` | Выполните команду на указанном удаленном компьютере. |
| -config `<value>` | Указывает файл параметров, содержащий параметры команды. |
| [-n] `<name>` | Задает имя целевого объекта. |
| -ETS | Отправляет команды в сеансы трассировки событий напрямую, без сохранения или планирования. |
| — как | Выполняет запрошенную операцию асинхронно. |
| -? | Отображает контекстную справку. |

### <a name="examples"></a>Примеры

Чтобы запустить сборщик данных *perf_log*, на удаленном компьютере *server_1* введите:

```
logman start perf_log -s server_1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда logman](logman.md)
