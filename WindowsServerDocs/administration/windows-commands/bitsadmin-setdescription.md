---
title: bitsadmin setdescription
description: Справочная статья по команде битсадмин SetDescription, которая задает описание указанного задания.
ms.topic: reference
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a306605d447a3bc3a40b16f75a1a63badf75f3b0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630943"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

Задает описание для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| description | Текст, используемый для описания задания. |

## <a name="examples"></a>Примеры

Чтобы получить описание задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
