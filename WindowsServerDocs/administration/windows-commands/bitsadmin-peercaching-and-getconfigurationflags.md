---
title: bitsadmin peercaching и getconfigurationflags
description: Справочная статья для команды битсадмин и жетконфигуратионфлагс, которая получает флаги конфигурации, которые определяют, обслуживает ли компьютер содержимое одноранговым узлам, а также может ли он скачивать содержимое с одноранговых узлов.
ms.topic: reference
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 064d6e5cfa0b59e11986263714039fab39e0b402
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821418"
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
