---
title: bdehdcfg target
description: Справочная статья по команде BdeHdCfg Target, которая готовит раздел для использования в качестве системного диска с помощью BitLocker и восстановления Windows.
ms.topic: reference
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7cc13e3c224aa1af944c5e9c9550737addcb6980
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632814"
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
