---
title: Manage-bde выкл.
description: Справочная статья по команде Manage-bde Off, которая расшифровывает диск и отключает BitLocker.
ms.topic: reference
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 94defd0e9393879d1ee6d9dd38201d079faad55c
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101812731"
---
# <a name="manage-bde-off"></a>Manage-bde выкл.

Расшифровывает диск и отключает BitLocker. Все предохранители ключа удаляются после завершения расшифровки.

## <a name="syntax"></a>Синтаксис

```
manage-bde -off [<volume>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<volume>` | Указывает букву диска, за которой следует двоеточие, путь GUID тома или подключенный том. |
| -ComputerName | Указывает, что manage-bde.exe будет использоваться для изменения защиты BitLocker на другом компьютере. Можно также использовать параметр **-CN** в качестве сокращенной версии этой команды. |
| `<name>` | Представляет имя компьютера, на котором необходимо изменить защиту BitLocker. Допустимые значения включают имя NetBIOS компьютера и IP-адрес компьютера. |
| -? или/? | Отображает краткую справку в командной строке. |
| -Help или-h | Отображает полную справку в командной строке. |

### <a name="examples"></a>Примеры

Чтобы отключить BitLocker на диске C, введите:

```
manage-bde –off C:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Manage-bde в команде](manage-bde-on.md)

- [Команда управления-BDE Pause](manage-bde-pause.md)

- [Команда управления-bde resume](manage-bde-resume.md)

- [Команда Manage-bde](manage-bde.md)
