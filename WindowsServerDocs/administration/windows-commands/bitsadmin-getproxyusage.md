---
title: bitsadmin getproxyusage
description: Справочная статья по команде битсадмин жетпроксюсаже, которая получает параметр использования прокси-сервера для указанного задания.
ms.topic: reference
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 423168d72a88ecad90fd8de43eab3cb4486a750b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024408"
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
