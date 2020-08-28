---
title: bdehdcfg restart
description: Справочная статья для команды перезапуска BdeHdCfg, которая сообщает BdeHdCfg о необходимости перезагрузки компьютера после завершения подготовки диска.
ms.topic: reference
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8db8ede29d5cecfdbe29031c21f86c5e2b8fc8c1
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031492"
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
