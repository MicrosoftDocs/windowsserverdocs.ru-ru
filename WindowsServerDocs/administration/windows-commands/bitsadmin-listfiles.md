---
title: bitsadmin listfiles
description: Справочная статья по команде битсадмин листфилес, в которой перечислены файлы в указанном задании.
ms.topic: reference
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 73c2e94ce9872aa05b2c0c897c678e3b1797ffc3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821468"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Перечисляет файлы в указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить список файлов для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
