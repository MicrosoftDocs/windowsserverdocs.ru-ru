---
title: exit
description: Справочная статья для выхода, которая выходит из интерпретатора команд.
ms.topic: article
ms.assetid: d3cee4a2-6210-46f0-b8e4-7381c3c4e530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 058e41d49ece470421fbd2b160037885b92c1bed
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890470"
---
# <a name="exit"></a>exit

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выход из интерпретатора команд или текущего пакетного скрипта.

## <a name="syntax"></a>Синтаксис

```
exit [/b] [<exitcode>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
