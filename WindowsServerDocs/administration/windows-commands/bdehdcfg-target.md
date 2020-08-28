---
title: bdehdcfg target
description: Справочная статья по команде BdeHdCfg Target, которая готовит раздел для использования в качестве системного диска с помощью BitLocker и восстановления Windows.
ms.topic: reference
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 173dfa5a8e873b76e512ce1d657eb1d51391640a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031472"
---
# <a name="bdehdcfg-target"></a>BdeHdCfg: целевой объект

Подготавливает раздел для использования в качестве системного диска с помощью BitLocker и восстановления Windows. По умолчанию эта секция создается без буквы диска.

## <a name="syntax"></a>Синтаксис

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| default | Указывает, что программа командной строки будет следовать тому же процессу, что и мастер установки BitLocker. |
| нераспределенного | Создает системный раздел из нераспределенного пространства, доступного на диске. |
| `<drive_letter>` соответствии | Сокращает диск, указанный объемом, необходимым для создания активного системного раздела. Чтобы использовать эту команду, на указанном диске должно быть не менее 5% свободного места. |
| `<drive_letter>` AutoMerge | Использует диск, указанный в качестве активного системного раздела. Диск операционной системы не может быть целевым объектом для слияния. |

## <a name="examples"></a>Примеры

Чтобы назначить существующий диск (P) системным диском, сделайте следующее:

```
bdehdcfg -target P: merge
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
