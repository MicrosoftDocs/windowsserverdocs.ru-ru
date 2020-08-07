---
title: fsutil transaction
description: Справочная статья по команде fsutil Transaction, которая управляет транзакциями NTFS.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f70281af6ecf652cc1dba95ec09b07529f71752e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889795"
---
# <a name="fsutil-transaction"></a>fsutil transaction

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Управляет транзакциями NTFS.

## <a name="syntax"></a>Синтаксис

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <filename>
fsutil transaction [list]
fsutil transaction [query] [{files | all}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| фиксация | Помечает конец успешной явной или явно указанной транзакции. |
| `<GUID>` | Указывает значение GUID, представляющее транзакцию. |
| FileInfo  | Отображает сведения о транзакциях для указанного файла. |
| `<filename>` | Указывает полный путь и имя файла. |
| list | Отображает список выполняющихся в данный момент транзакций. |
| query | Отображает сведения для указанной транзакции.<ul><li>Если `fsutil transaction query files` указан параметр, сведения о файле отображаются только для указанной транзакции.</li><li>Если `fsutil transaction query all` указан параметр, будут отображены все сведения о транзакции.</li></ul> |
| откат; | Выполняет откат указанной транзакции к началу. |

### <a name="examples"></a>Примеры

Чтобы отобразить сведения о транзакции для *c:\test.txt*файлов, введите:

```
fsutil transaction fileinfo c:\test.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Поддержка транзакций в NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v=ws.10))
