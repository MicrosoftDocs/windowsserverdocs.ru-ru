---
title: bitsadmin setpriority
description: Справочная статья по команде битсадмин SetPriority, которая задает приоритет указанного задания.
ms.topic: reference
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 25bf7026ceef21fb37824ce99f56389941426b79
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630725"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

Задает приоритет указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setpriority <job> <priority>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| priority | Задает приоритет задания, включая:<ul><li>FOREGROUND</li><li>HIGH.</li><li>NORMAL</li><li>LOW</li></ul> |

## <a name="examples"></a>Примеры

Чтобы задать приоритет для задания с именем *мидовнлоаджоб* , выполните следующие действия.

```
bitsadmin /setpriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
