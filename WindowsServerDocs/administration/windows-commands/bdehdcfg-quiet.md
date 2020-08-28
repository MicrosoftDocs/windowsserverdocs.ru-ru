---
title: bdehdcfg quiet
description: Справочная статья по команде BdeHdCfg quiet, которая указывает, что BdeHdCfg не отображает все действия и ошибки.
ms.topic: reference
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 842788b4413cda828d208e8e7fbbeed28d7a72be
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031532"
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
