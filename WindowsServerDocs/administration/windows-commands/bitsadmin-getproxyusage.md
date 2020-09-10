---
title: bitsadmin getproxyusage
description: Справочная статья по команде битсадмин жетпроксюсаже, которая получает параметр использования прокси-сервера для указанного задания.
ms.topic: reference
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bdfcfa92a5886857920d56a0028a450ee9a3e521
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631729"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

Извлекает параметр использования прокси-сервера для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

#### <a name="output"></a>Выходные данные

Возвращаемые значения использования прокси-сервера могут быть:

- Предварительная **Настройка** — используйте значения по умолчанию для свойства Owner в Internet Explorer.

- **No_Proxy** — не использовать прокси-сервер.

- **Reoverride** — Используйте явный список прокси-серверов.

- **Автообнаружение** — автоматическое определение параметров прокси-сервера.

## <a name="examples"></a>Примеры

Чтобы получить сведения об использовании прокси-сервера для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
