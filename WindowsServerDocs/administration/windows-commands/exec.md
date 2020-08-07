---
title: exec
description: Справочная статья по команде Exec, которая запускает файл скрипта на локальном компьютере.
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d0fd297ca3b5908a6782379dbd716098e47f751
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890490"
---
# <a name="exec"></a>exec

Запускает файл скрипта на локальном компьютере. Эта команда также дублирует или восстанавливает данные в рамках последовательности резервного копирования или восстановления. В случае сбоя скрипта возвращается ошибка, и сценарий DiskShadow завершает работу.

Файл может быть сценарием **cmd** .

## <a name="syntax"></a>Синтаксис

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<scriptfile.cmd>` | Указывает запускаемый файл скрипта. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Diskshadow, команда](diskshadow.md)
