---
title: nslookup set retry
description: Справочная статья по команде nslookup set retry, которая задает число попыток получения сведений с указанного сервера.
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b4449be93c4587dcb5d1a7990a79352a1fa7b28
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885551"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Если ответ не получен в течение определенного промежутка времени, интервал времени ожидания удваивается, и запрос отсылается повторно. Эта команда задает количество повторных попыток отправки запроса на сервер для получения сведений.

> [!NOTE]
> Чтобы изменить продолжительность времени до истечения времени ожидания запроса, используйте команду [nslookup set timeout](nslookup-set-timeout.md) .

## <a name="syntax"></a>Синтаксис

```
set retry=<number>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| ---------- | ---------- |
| `<number>` | Указывает новое значение для числа повторных попыток. По умолчанию число повторных попыток равно **4**. |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set timeout](nslookup-set-timeout.md)
