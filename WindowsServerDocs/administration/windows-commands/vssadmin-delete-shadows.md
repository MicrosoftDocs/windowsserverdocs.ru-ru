---
title: vssadmin delete shadows
description: Описание команды vssadmin Delete Shadows, которая удаляет теневые копии указанного тома.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2dcd1bf8cbe946c77d0b5a100d2a29ecb36ef50f
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156227"
---
# <a name="vssadmin-delete-shadows"></a>vssadmin delete shadows

> Область применения: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Удаляет теневые копии указанного тома. Удалять можно только теневые копии с типом, *доступным для клиента* .

## <a name="syntax"></a>Синтаксис

```
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /фор =`<ForVolumeSpec>` | Указывает, какой из теневых копий тома будет удален. |
| /олдест | Удаляет только самую старую теневую копию. |
| /all | Удаляет все заданные теневые копии тома. |
| /Шадов =`<ShadowID>` | Удаляет теневую копию, указанную параметром Шадовид. Чтобы получить идентификатор теневой копии, используйте [команду vssadmin List Shadows](vssadmin-list-shadows.md). При вводе идентификатора теневой копии используйте следующий формат, где каждый *X* представляет шестнадцатеричный символ:<p>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX |
| /quiet | Указывает, что команда не будет отображать сообщения во время выполнения. |

## <a name="examples"></a>Примеры

Чтобы удалить самую старую теневую копию тома C, введите:

```
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [vssadmin, команда](vssadmin.md)

- [Команда VSSadmin list Shadows](vssadmin-list-shadows.md)
