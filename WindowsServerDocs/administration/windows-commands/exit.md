---
title: exit
description: Справочная статья для выхода, которая выходит из интерпретатора команд.
ms.topic: reference
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 171ed258c266b203495d142b80d19adeec79e464
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818308"
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
