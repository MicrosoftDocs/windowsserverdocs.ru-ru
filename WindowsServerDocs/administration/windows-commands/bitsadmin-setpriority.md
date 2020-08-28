---
title: bitsadmin setpriority
description: Справочная статья по команде битсадмин SetPriority, которая задает приоритет указанного задания.
ms.topic: reference
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1fe6a2b3981697a4a8c287fe4fb49c31a4f4244
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028472"
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
