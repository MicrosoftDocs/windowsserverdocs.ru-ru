---
title: bitsadmin geterrorcount
description: Справочная статья по команде битсадмин жетерроркаунт, которая извлекает количество раз, когда указанное задание создало временную ошибку.
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8cfe0065ca9cec6d903466428b78cb8c103de5e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894348"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

Извлекает число раз, когда указанное задание создало временную ошибку.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить сведения о количестве ошибок для задания с именем *мидовнлоаджоб*:

```
bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
