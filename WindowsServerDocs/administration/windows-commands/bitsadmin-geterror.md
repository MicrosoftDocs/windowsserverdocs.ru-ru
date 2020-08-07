---
title: bitsadmin geterror
description: Справочная статья по команде битсадмин Error, которая получает подробные сведения об ошибке для указанного задания.
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae0b2391267ddc1508d8343b909b9739a0e01ffb
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894352"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Извлекает подробные сведения об ошибке для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить сведения об ошибке для задания с именем *мидовнлоаджоб*:

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
