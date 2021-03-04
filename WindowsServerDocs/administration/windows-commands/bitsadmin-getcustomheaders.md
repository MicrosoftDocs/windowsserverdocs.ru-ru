---
title: bitsadmin getcustomheaders
description: Справочная статья по команде битсадмин жеткустомхеадерс, которая получает пользовательские заголовки HTTP из задания.
ms.topic: reference
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b3037fe391b42a36aba608c34f7d0274d24a4d32
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822188"
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
