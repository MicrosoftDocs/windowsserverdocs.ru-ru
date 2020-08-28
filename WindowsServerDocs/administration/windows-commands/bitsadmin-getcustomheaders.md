---
title: bitsadmin getcustomheaders
description: Справочная статья по команде битсадмин жеткустомхеадерс, которая получает пользовательские заголовки HTTP из задания.
ms.topic: reference
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09bd1f43e54c6fbca39dffe7c89b978b2b0d2944
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033662"
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
