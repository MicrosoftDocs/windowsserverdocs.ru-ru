---
title: bitsadmin replaceremoteprefix
description: Справочная статья по команде битсадмин реплацеремотепрефикс, при необходимости которая изменяет удаленный URL-адрес для всех файлов в задании с *олдпрефикс* на *невпрефикс*.
ms.topic: reference
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 882c42e439393fcc4e9bb093209036465a838a41
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821188"
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
