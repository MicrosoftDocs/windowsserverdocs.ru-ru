---
title: lodctr
description: Справочная статья по команде lodctr, которая позволяет зарегистрировать или сохранить имя счетчика производительности и параметры реестра в файле и назначить Доверенные службы.
ms.topic: reference
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7a222935d61f33ce66b76cba2a9852e439a76d9b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814151"
---
# <a name="lodctr"></a>lodctr

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет зарегистрировать или сохранить имя счетчика производительности и параметры реестра в файле и назначить Доверенные службы.

## <a name="syntax"></a>Синтаксис

```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<filename>` | Задает имя файла инициализации, который регистрирует параметры имени счетчика производительности и пояснительный текст. |
| ключ`<filename>` | Задает имя файла, в котором сохраняются параметры реестра счетчика производительности и пояснительный текст. |
| /r | Восстанавливает параметры реестра счетчиков и пояснительный текст из текущих параметров реестра и кэшированных файлов производительности, связанных с реестром. |
| /r`<filename>` | Указывает имя файла, который восстанавливает параметры реестра счетчика производительности и пояснительный текст.<p>**Предупреждение:** При использовании этой команды будут перезаписаны все параметры реестра счетчиков производительности и пояснительный текст, заменяя их конфигурациями, определенными в указанном файле. |
| /t:`<servicename>` | Указывает, что служба `<servicename>` является доверенной. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Если предоставленные сведения содержат пробелы, заключите его в кавычки (например, "имя файла 1").

### <a name="examples"></a>Примеры

Чтобы сохранить текущие параметры реестра производительности и пояснительный текст к файлу *"perf backup1.txt"*, введите:

```
lodctr /s:"perf backup1.txt"
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
