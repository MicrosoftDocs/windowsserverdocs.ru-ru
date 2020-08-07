---
title: bitsadmin peercaching и getconfigurationflags
description: Справочная статья для команды битсадмин и жетконфигуратионфлагс, которая получает флаги конфигурации, которые определяют, обслуживает ли компьютер содержимое одноранговым узлам, а также может ли он скачивать содержимое с одноранговых узлов.
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 383387b135f38663a84999e041a4f6864d40a01d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893628"
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
