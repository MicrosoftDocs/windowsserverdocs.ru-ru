---
title: bitsadmin geterrorcount
description: Справочная статья по команде битсадмин жетерроркаунт, которая извлекает количество раз, когда указанное задание создало временную ошибку.
ms.topic: reference
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b2a9485c58658d06f5af7b46c2289a0051b0cc51
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822048"
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
