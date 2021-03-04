---
title: endlocal
description: Справочная статья по команде endlocal, которая завершает локализацию изменений среды в пакетном файле и восстанавливает значения переменных среды перед выполнением соответствующей команды setlocal.
ms.topic: reference
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4d84efe79bec1254a2d5c25ef26492e7b0c2bc6a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818438"
---
# <a name="endlocal"></a>endlocal

Завершает локализацию изменений среды в пакетном файле и восстанавливает значения переменных среды перед выполнением соответствующей команды **setlocal** .

## <a name="syntax"></a>Синтаксис

```
endlocal
```

### <a name="parameters"></a>Параметры

| Параметр | Description |
| --------- | ----------- |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Команда **endlocal** не действует вне сценария или пакетного файла.

- В конце пакетного файла имеется неявная команда **endlocal** .

- Если расширения команд включены (по умолчанию включены расширения команд), команда **endlocal** восстанавливает состояние расширений команд (то есть включено или отключено) до выполнения команды **setlocal** .

> [!NOTE]
> Дополнительные сведения о включении и отключении расширений команд см. в описании [команды cmd](cmd.md).

### <a name="examples"></a>Примеры

Можно локализовать переменные среды в пакетном файле. Например, следующая программа запускает пакетную программу *суперапп* в сети, направляет выходные данные в файл и отображает его в блокноте:

```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
