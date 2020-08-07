---
title: fsutil volume
description: Справочная статья по команде fsutil volume, которая отключает том или запрашивает жесткий диск, чтобы определить, какой объем свободного места в данный момент доступен на жестком диске или какой файл используется в конкретном кластере.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b6bcd763643eba8c82fbd1ebd82199aa46f8f0dd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889753"
---
# <a name="fsutil-volume"></a>fsutil volume

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Отключает том или запрашивает жесткий диск, чтобы определить, какой объем свободного места в настоящее время доступен на жестком диске или какой файл используется в конкретном кластере.

## <a name="syntax"></a>Синтаксис

```
fsutil volume [allocationreport] <volumepath>
fsutil volume [diskfree] <volumepath>
fsutil volume [dismount] <volumepath>
fsutil volume [filelayout] <volumepath> <fileID>
fsutil volume [list]
fsutil volume [querycluster] <volumepath> <cluster> [<cluster>] … …
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| аллокатионрепорт | Отображает сведения о том, как хранилище используется на заданном томе. |
| `<volumepath>` | Указывает букву диска (с последующим двоеточием). |
| дискфри | Запрашивает жесткий диск, чтобы определить объем свободного места на нем. |
| отключить | Отключает том. |
| филелайаут | Отображает метаданные NTFS для заданного файла. |
| `<fileID>` | Указывает идентификатор файла. |
| list | Список всех томов в системе. |
| куериклустер | Определяет, какой файл использует указанный кластер. Можно указать несколько кластеров с помощью параметра **куериклустер** . |
| `<cluster>` | Указывает номер логического кластера (LCN). |

### <a name="examples"></a>Примеры

Чтобы отобразить отчет о распределенных кластерах, введите:

```
fsutil volume allocationreport C:
```

Чтобы отключить том на диске C, введите:

```
fsutil volume dismount c:
```

Чтобы запросить объем свободного пространства тома на диске C, введите:

```
fsutil volume diskfree c:
```

Чтобы отобразить все сведения о указанных файлах, введите:

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

Чтобы вывести список томов на диске, введите:

```
fsutil volume list
```

Чтобы найти файлы, использующие кластеры, указанные номерами логических кластеров 50 и 0x2000 на диске C, введите:

```
fsutil volume querycluster C: 50 0x2000
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Как работает NTFS](/previous-versions/windows/it-pro/windows-server-2003/cc781134(v=ws.10))
