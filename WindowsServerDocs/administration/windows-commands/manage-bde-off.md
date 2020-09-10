---
title: Manage-bde выкл.
description: Справочная статья по команде Manage-bde Off, которая расшифровывает диск и отключает BitLocker.
ms.topic: reference
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8802b971b6d63e6f0693b6b40222c325ab576bc3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639655"
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
