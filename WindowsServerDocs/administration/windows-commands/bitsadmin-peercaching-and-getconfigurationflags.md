---
title: bitsadmin peercaching и getconfigurationflags
description: Справочная статья для команды битсадмин и жетконфигуратионфлагс, которая получает флаги конфигурации, которые определяют, обслуживает ли компьютер содержимое одноранговым узлам, а также может ли он скачивать содержимое с одноранговых узлов.
ms.topic: reference
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3fe1adfb44ab845ecdb73222131191782f83c075
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631370"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin peercaching и getconfigurationflags

Получает флаги конфигурации, которые определяют, обслуживает ли компьютер содержимое одноранговым узлам, и может ли он скачивать содержимое с одноранговых узлов.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить флаги конфигурации для задания с именем *мидовнлоаджоб*:

```
bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)

- [Команда кэширования битсадмин](bitsadmin-peercaching.md)
