---
title: bitsadmin getminretrydelay
description: Справочная статья по команде битсадмин жетминретриделай, которая получает время ожидания (в секундах), в течение которого служба будет ожидать временной ошибки, прежде чем пытаться переместить файл.
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89e925dd8db3932e273552a82a497d99fd3bdb95
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894191"
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
