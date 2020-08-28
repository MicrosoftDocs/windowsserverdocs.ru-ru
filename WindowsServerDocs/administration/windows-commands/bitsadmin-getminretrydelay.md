---
title: bitsadmin getminretrydelay
description: Справочная статья по команде битсадмин жетминретриделай, которая получает время ожидания (в секундах), в течение которого служба будет ожидать временной ошибки, прежде чем пытаться переместить файл.
ms.topic: reference
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f5bc6d69e7dbc46bc7e0df3a34ac97f37fda252
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030312"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

Возвращает продолжительность времени в секундах, в течение которого служба будет ожидать после возникновения временной ошибки, прежде чем пытаться переместить файл.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Для получения минимальной задержки повтора для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
