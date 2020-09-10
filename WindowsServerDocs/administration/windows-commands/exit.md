---
title: exit
description: Справочная статья для выхода, которая выходит из интерпретатора команд.
ms.topic: reference
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c1fbf37b80c55a9620c2e72d20ea13c6766b7da9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635951"
---
# <a name="exit"></a>exit

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выход из интерпретатора команд или текущего пакетного скрипта.

## <a name="syntax"></a>Синтаксис

```
exit [/b] [<exitcode>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /b | Выход из текущего пакетного скрипта вместо выхода из Cmd.exe. Если выполняется из-за пределов пакетного скрипта, выполняет выход из Cmd.exe. |
| `<exitcode>` | Указывает числовое число. Если указан параметр **/b** , переменной среды ERRORLEVEL присваивается это число. Если интерпретатор команд закрывается, код завершения процесса устанавливается в это число. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы закрыть интерпретатор команд, введите:

```
exit
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
