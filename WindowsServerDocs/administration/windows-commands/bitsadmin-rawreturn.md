---
title: bitsadmin rawreturn
description: Справочная статья по команде битсадмин равретурн, которая возвращает данные, подходящие для синтаксического анализа.
ms.topic: reference
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 89542ca02b78471b4c566dd821025ad15fd569e9
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821228"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Возвращает данные, подходящие для синтаксического анализа. Как правило, эта команда используется совместно с параметрами **/CREATE** и **/Get*** для получения только значения. Этот параметр необходимо указать перед другими коммутаторами.

> [!NOTE]
> Эта команда удаляет символы новой строки и форматирование из выходных данных.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /rawreturn
```

## <a name="examples"></a>Примеры

Чтобы получить необработанные данные для состояния задания с именем *мидовнлоаджоб*:

```
bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
