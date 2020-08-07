---
title: fsutil wim
description: Справочная статья по команде fsutil WIM, которая предоставляет функции для обнаружения и управления файлами, поддерживающими образ Windows (WIM).
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f709ec86924f24e7321e4de14d3e21615f207903
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889749"
---
# <a name="fsutil-wim"></a>fsutil wim

> Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2019, Windows Server 2016, Windows 10

Предоставляет функции для обнаружения и управления файлами, поддерживающими образ Windows (WIM).

## <a name="syntax"></a>Синтаксис

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| енумфилес | Перечисляет файлы с резервным копированием WIM. |
| `<drive name>` | Указывает имя диска. |
| `<data source>` | Указывает источник данных. |
| енумвимс | Перечисляет резервные WIM-файлы. |
| куерифиле | Запросы, если файл поддерживается WIM, и, если это так, отображает сведения о WIM-файле. |
| `<filename>` | Указывает имя файла. |
| ремовевим | Удаляет WIM из резервных файлов. |

### <a name="examples"></a>Примеры

Чтобы перечислить файлы для диска C: из источника данных 0, введите:

```
fsutil wim enumfiles C: 0
```

Чтобы перечислить резервные WIM-файлы для диска C:, введите:

```
fsutil wim enumwims C:
```

Чтобы узнать, поддерживается ли файл WIM, введите:

```
fsutil wim C:\Windows\Notepad.exe
```

Чтобы удалить WIM из резервных файлов для тома C: и источника данных 2, введите:

```
fsutil wim removewims C: 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [fsutil](fsutil.md)
