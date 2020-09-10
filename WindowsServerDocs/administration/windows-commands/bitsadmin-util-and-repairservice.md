---
title: bitsadmin util и repairservice
description: Справочная статья по команде битсадмин util and репаирсервице, которая устраняет известные проблемы в различных версиях службы BITS.
ms.topic: reference
ms.assetid: 2ac7baeb-4340-4186-bfcb-66478195378d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0bef08a3e0db8973de9370279144be5951445cc3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630447"
---
# <a name="bitsadmin-util-and-repairservice"></a>bitsadmin util и repairservice

Если не удается запустить службу BITS, этот параметр пытается устранить ошибки, связанные с неправильной конфигурацией службы и зависимостями в службах Windows (например, LANManworkstation) и в сетевом каталоге. Этот параметр также создает выходные данные, указывающие, разрешены ли проблемы.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,5 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /util /repairservice [/force]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /Force | Необязательный параметр. Удаляет и создает службу снова.|

> [!NOTE]
> Если служба BITS вновь создает службу, строка описания службы может быть задана как английская даже в локализованной системе.

## <a name="examples"></a>Примеры

Чтобы восстановить конфигурацию службы BITS, выполните следующие действия.

```
bitsadmin /util /repairservice
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [битсадмин util, команда](bitsadmin-util.md)

- [Команда битсадмин](bitsadmin.md)
