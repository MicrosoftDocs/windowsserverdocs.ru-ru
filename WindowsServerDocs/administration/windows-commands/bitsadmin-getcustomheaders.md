---
title: bitsadmin getcustomheaders
description: Справочная статья по команде битсадмин жеткустомхеадерс, которая получает пользовательские заголовки HTTP из задания.
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3cc970a7aeee1be678a3c77d852af91ae0ab98c8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894414"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

Извлекает из задания пользовательские заголовки HTTP.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Для получения пользовательских заголовков для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
