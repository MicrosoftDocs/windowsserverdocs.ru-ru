---
title: bitsadmin replaceremoteprefix
description: Справочная статья по команде битсадмин реплацеремотепрефикс, при необходимости которая изменяет удаленный URL-адрес для всех файлов в задании с *олдпрефикс* на *невпрефикс*.
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86149b09c65f430bf0a3bbe7a1595bb5385c6dcc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893362"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

При необходимости изменяет удаленный URL-адрес для всех файлов в задании с *олдпрефикс* на *невпрефикс*.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| олдпрефикс | Существующий префикс URL-адреса. |
| невпрефикс | Новый префикс URL-адреса. |

## <a name="examples"></a>Примеры

Чтобы изменить удаленный URL-адрес для всех файлов в задании с именем *мидовнлоаджоб*, с *http://stageserver* на *http://prodserver* .

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Дополнительные сведения

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
