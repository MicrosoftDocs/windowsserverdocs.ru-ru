---
title: Управление — BDE чанжепин
description: Справочная статья по команде Manage-bde чанжепин, которая изменяет ПИН-код для диска операционной системы.
ms.topic: reference
ms.assetid: c85aa1c7-3485-4839-a292-99dfcd6db252
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 001f934e55e8b78cae5800dda59ec5d5a12fb606
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033982"
---
# <a name="manage-bde-changepin"></a>Управление — BDE чанжепин

Изменяет ПИН-код для диска операционной системы. Пользователю предлагается ввести новый ПИН-код.

## <a name="syntax"></a>Синтаксис

```
manage-bde -changepin [<drive>] [-computername <name>] [{-?|/?}] [{-help|-h}]
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

Чтобы изменить ПИН-код, используемый BitLocker на диске C, введите:

```
manage-bde –changepin C:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Manage-bde](manage-bde.md)
