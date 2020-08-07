---
title: bitsadmin makecustomheaderswriteonly
description: Справочная статья по команде битсадмин макекустомхеадерсвритеонли, которая делает пользовательские заголовки HTTP для задания только для записи.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b1e152ee51f3009a5cc1f5bf1b747e65e86e5e04
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893692"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

Сделайте пользовательские HTTP-заголовки задания только для записи.

> [!IMPORTANT]
> Это действие нельзя отменить.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы сделать пользовательские заголовки HTTP только для записи для задания с именем *мидовнлоаджоб*, сделайте следующее:

```
bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
