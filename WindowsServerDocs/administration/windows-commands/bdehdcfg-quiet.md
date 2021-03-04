---
title: bdehdcfg quiet
description: Справочная статья по команде BdeHdCfg quiet, которая указывает, что BdeHdCfg не отображает все действия и ошибки.
ms.topic: reference
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1eb3b2db87de32fdf3fc9e5c721ac1fcb0f5dfc7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822798"
---
# <a name="bdehdcfg-quiet"></a>BdeHdCfg: тихий режим

Информирует программу командной строки BdeHdCfg о том, что все действия и ошибки не должны отображаться в интерфейсе командной строки. Любые запросы да/нет (Y/N), отображаемые во время подготовки диска, принимают ответ "Да". Чтобы просмотреть ошибки, возникшие во время подготовки диска, просмотрите журнал системных событий в поставщике событий **Microsoft-Windows-BitLocker-дривепрепаратионтул** .

## <a name="syntax"></a>Синтаксис

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -quiet
```

#### <a name="parameters"></a>Параметры

У этой команды нет дополнительных параметров.

## <a name="examples"></a>Примеры

Чтобы использовать команду **quiet** , выполните следующие действия:

```
bdehdcfg -target default -quiet
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
