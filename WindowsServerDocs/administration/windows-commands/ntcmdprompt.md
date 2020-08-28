---
title: ntcmdprompt
description: Справочная статья по команде нткмдпромпт, которая запускает интерпретатор команд **Cmd.exe**, а не **Command.com**, после выполнения команды завершения и сохранения резидентных (резидентных) программ или после запуска командной строки в приложении MS-DOS.
ms.topic: reference
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 557db55ea99b209f2bca152f1e45622aa0df4887
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032762"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает интерпретатор команд **Cmd.exe**, а не **Command.com**, после завершения и поддержания резидентных (резидентных) программ или после запуска командной строки в приложении MS-DOS.

## <a name="syntax"></a>Синтаксис

```
ntcmdprompt
```

### <a name="parameters"></a>Параметры

| Параметр | Description |
| --------- | ----------- |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Remarks

- Когда **Command.com** работает, некоторые функции **Cmd.exe**, например, отображение журнала команд **Doskey** , недоступны. Если вы предпочитаете запустить интерпретатор команд **Cmd.exe** после начала и сохранения резидентных (резидентных) программ или запуска Командная строка из приложения на основе MS-DOS, можно использовать команду **нткмдпромпт** . Однако помните, что РЕЗИДЕНТная программа может быть недоступна для использования при работе **Cmd.exe**. Команду **нткмдпромпт** можно включить в файл **config. NT** или в эквивалентный пользовательский файл запуска в файле сведений о программе (PIF) приложения.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
