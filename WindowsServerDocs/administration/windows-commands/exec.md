---
title: exec
description: Справочная статья по команде Exec, которая запускает файл скрипта на локальном компьютере.
ms.topic: reference
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 840829584299826bd30007347251485760b1cce8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818358"
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
