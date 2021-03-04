---
title: bitsadmin setdescription
description: Справочная статья по команде битсадмин SetDescription, которая задает описание указанного задания.
ms.topic: reference
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4aaa4e281693414f69aa4f2e53bb9bb26eddceca
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821028"
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
| description; | Текст, используемый для описания задания. |

## <a name="examples"></a>Примеры

Чтобы получить описание задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
