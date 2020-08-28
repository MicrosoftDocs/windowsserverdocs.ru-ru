---
title: bitsadmin replaceremoteprefix
description: Справочная статья по команде битсадмин реплацеремотепрефикс, при необходимости которая изменяет удаленный URL-адрес для всех файлов в задании с *олдпрефикс* на *невпрефикс*.
ms.topic: reference
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21c1ede5b05a80ba80b1bd470065e914fb353c3c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026332"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

При необходимости изменяет удаленный URL-адрес для всех файлов в задании с *олдпрефикс* на *невпрефикс*.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
