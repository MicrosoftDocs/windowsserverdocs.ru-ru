---
title: bitsadmin setpriority
description: Справочная статья по команде битсадмин SetPriority, которая задает приоритет указанного задания.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 07afd9c636a5dbcd4e70de71b3a6f515e7e02bae
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927599"
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
