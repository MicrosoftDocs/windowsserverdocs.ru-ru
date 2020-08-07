---
title: bitsadmin getowner
description: Справочная статья по команде битсадмин, которая получает владельца указанного задания.
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91dd63dcba8b41fee01c17e87c817e32a9dbba39
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894050"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

Отображает отображаемое имя или идентификатор GUID владельца указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы отобразить владельца для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
