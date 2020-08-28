---
title: exec
description: Справочная статья по команде Exec, которая запускает файл скрипта на локальном компьютере.
ms.topic: reference
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0e4cd876fe5c6abcf909f20e330ff347db1113b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023998"
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
