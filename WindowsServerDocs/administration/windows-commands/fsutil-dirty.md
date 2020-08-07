---
title: fsutil dirty
description: Справочная статья по команде fsutil dirty, которая запрашивает или устанавливает «грязный» бит тома.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 00fd11e577957e45bb8b2491b54cf1548effedc3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890003"
---
# <a name="fsutil-dirty"></a>fsutil dirty

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Запрашивает или устанавливает «грязный» бит тома. Если задан «грязный» бит тома, то **Autochk** автоматически проверяет том на наличие ошибок при следующем перезапуске компьютера.

## <a name="syntax"></a>Синтаксис

```
fsutil dirty {query | set} <volumepath>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| query | Запрашивает «грязный» бит указанного тома. |
| set | Задает "грязный" бит указанного тома. |
| `<volumepath>` | Указывает имя диска, за которым следует двоеточие или GUID в следующем формате: `volume{GUID}` . |

#### <a name="remarks"></a>Remarks

- «Грязный» бит тома означает, что файловая система может находиться в нестабильном состоянии. "Грязный" бит можно задать по следующим причинам:

    - Том находится в режиме "в сети" и содержит необработанные изменения.

    - Внесены изменения в том, и компьютер был завершен до того, как изменения были зафиксированы на диске.

    - На томе обнаружено повреждение.

- Если «грязный» бит задан при перезапуске компьютера, **chkdsk** запускается для проверки целостности файловой системы и попыток устранения любых проблем с томом.

### <a name="examples"></a>Примеры

Чтобы запросить "грязный" бит на диске C, введите:

```
fsutil dirty query c:
```

- Если том изменен, отображается следующий результат:`Volume C: is dirty`

- Если том не является "грязным", отображаются следующие выходные данные:`Volume C: is not dirty`

Чтобы установить «грязный» бит на диске C, введите:

```
fsutil dirty set C:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [fsutil](fsutil.md)
