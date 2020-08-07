---
title: bitsadmin getproxyusage
description: Справочная статья по команде битсадмин жетпроксюсаже, которая получает параметр использования прокси-сервера для указанного задания.
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff2320ba66cdc11781ac56900e5a4aaa9fb1dc0f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893933"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

Извлекает параметр использования прокси-сервера для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
