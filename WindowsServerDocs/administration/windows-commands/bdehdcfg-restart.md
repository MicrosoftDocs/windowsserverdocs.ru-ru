---
title: bdehdcfg restart
description: Справочная статья для команды перезапуска BdeHdCfg, которая сообщает BdeHdCfg о необходимости перезагрузки компьютера после завершения подготовки диска.
ms.topic: reference
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 41397b1e54c8f0ac1dcfc58888fb0594f7772492
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822788"
---
# <a name="bdehdcfg-restart"></a>BdeHdCfg: перезапуск

Информирует программу командной строки BdeHdCfg о том, что компьютер должен быть перезагружен после завершения подготовки диска. Если другие пользователи вошли в систему, а команда **quiet** не указана, появится запрос на подтверждение перезагрузки компьютера.

## <a name="syntax"></a>Синтаксис

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -restart
```

#### <a name="parameters"></a>Параметры

У этой команды нет дополнительных параметров.

## <a name="examples"></a>Примеры

Чтобы использовать команду **restart** , выполните следующие действия.

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
