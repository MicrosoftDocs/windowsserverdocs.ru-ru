---
title: Управление — блокировка BDE
description: Справочная статья по команде Manage-bde Lock, которая блокирует диск, защищенный BitLocker, чтобы предотвратить доступ к нему, если не указан ключ блокировки.
ms.topic: article
ms.assetid: b8858e61-3a7e-4d03-8c98-5c09853f35e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a1c7fd743832caaacec46ff2fdc7008983b8472
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886858"
---
# <a name="manage-bde-lock"></a>Управление — блокировка BDE

Блокирует защищенный BitLocker диск, чтобы предотвратить доступ к нему, если не указан ключ блокировки.

## <a name="syntax"></a>Синтаксис

```
manage-bde -lock [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<drive>` | Представляет букву диска, за которой следует двоеточие. |
| -ComputerName | Указывает, что manage-bde.exe будет использоваться для изменения защиты BitLocker на другом компьютере. Можно также использовать параметр **-CN** в качестве сокращенной версии этой команды. |
| `<name>` | Представляет имя компьютера, на котором необходимо изменить защиту BitLocker. Допустимые значения включают имя NetBIOS компьютера и IP-адрес компьютера. |
| -? или/? | Отображает краткую справку в командной строке. |
| -Help или-h | Отображает полную справку в командной строке. |

### <a name="examples"></a>Примеры

Чтобы заблокировать диск данных D, введите:

```
manage-bde –lock D:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Manage-bde](manage-bde.md)
