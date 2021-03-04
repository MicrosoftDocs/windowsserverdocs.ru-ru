---
title: Управление — возобновление BDE
description: Справочная статья по команде "Управление возобновлением с помощью BDE", которая возобновляет шифрование или расшифровку BitLocker после приостановки.
ms.topic: reference
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a5e2baa86dddee0d13d559784be509fbbbbba208
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101812671"
---
# <a name="manage-bde-resume"></a>Управление — возобновление BDE

Возобновляет шифрование или расшифровку BitLocker после его приостановки.

## <a name="syntax"></a>Синтаксис

```
manage-bde -resume [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<drive>` | Представляет букву диска, за которой следует двоеточие. |
| -ComputerName | Указывает, что manage-bde.exe будет использоваться для изменения защиты BitLocker на другом компьютере. Можно также использовать параметр **-CN** в качестве сокращенной версии этой команды. |
| `<name>` | Представляет имя компьютера, на котором необходимо изменить защиту BitLocker. Допустимые значения включают имя NetBIOS компьютера и IP-адрес компьютера. |
| -? или/? | Отображает краткую справку в командной строке. |
| -Help или-h | Отображает полную справку в командной строке. |

### <a name="examples"></a>Примеры

Чтобы возобновить шифрование BitLocker на диске C, введите:

```
manage-bde –resume C:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Manage-bde в команде](manage-bde-on.md)

- [Команда управления-BDE Off](manage-bde-off.md)

- [Команда управления-BDE Pause](manage-bde-pause.md)

- [Команда Manage-bde](manage-bde.md)
