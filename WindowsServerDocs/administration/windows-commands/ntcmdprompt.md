---
title: ntcmdprompt
description: Справочная статья по команде нткмдпромпт, которая запускает интерпретатор команд **Cmd.exe**, а не **Command.com**, после выполнения команды завершения и сохранения резидентных (резидентных) программ или после запуска командной строки в приложении MS-DOS.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a70a8cfdbe6e37bfb8d90bed23e961d100843506
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925343"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Запускает интерпретатор команд **Cmd.exe**, а не **Command.com**, после завершения и поддержания резидентных (резидентных) программ или после запуска командной строки в приложении MS-DOS.

## <a name="syntax"></a>Синтаксис

```
ntcmdprompt
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Когда **Command.com** работает, некоторые функции **Cmd.exe**, например, отображение журнала команд **Doskey** , недоступны. Если вы предпочитаете запустить интерпретатор команд **Cmd.exe** после начала и сохранения резидентных (резидентных) программ или запуска Командная строка из приложения на основе MS-DOS, можно использовать команду **нткмдпромпт** . Однако помните, что РЕЗИДЕНТная программа может быть недоступна для использования при работе **Cmd.exe**. Команду **нткмдпромпт** можно включить в файл **config. NT** или в эквивалентный пользовательский файл запуска в файле сведений о программе (PIF) приложения.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
