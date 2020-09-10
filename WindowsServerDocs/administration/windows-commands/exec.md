---
title: exec
description: Справочная статья по команде Exec, которая запускает файл скрипта на локальном компьютере.
ms.topic: reference
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 668dc3cf3d93d11066d7dece4309f586b3a5b964
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635963"
---
# <a name="exec"></a>exec

Запускает файл скрипта на локальном компьютере. Эта команда также дублирует или восстанавливает данные в рамках последовательности резервного копирования или восстановления. В случае сбоя скрипта возвращается ошибка, и сценарий DiskShadow завершает работу.

Файл может быть сценарием **cmd** .

## <a name="syntax"></a>Синтаксис

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<scriptfile.cmd>` | Указывает запускаемый файл скрипта. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Diskshadow, команда](diskshadow.md)
