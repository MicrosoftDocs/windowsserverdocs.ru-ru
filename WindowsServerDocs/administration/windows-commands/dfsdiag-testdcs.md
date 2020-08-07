---
title: dfsdiag testdcs
description: Справочная статья по команде дфсдиаг тестдкс, которая проверяет конфигурацию контроллеров домена в указанном домене.
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 762692e24231e04fe28e4fd9c1ac084b557653b1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891182"
---
# <a name="dfsdiag-testdcs"></a>dfsdiag testdcs

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Проверяет конфигурацию контроллеров домена, выполняя следующие тесты на каждом контроллере домена в указанном домене:

- Проверяет, запущена ли служба пространства имен распределенная файловая система (DFS), и имеет ли ее тип запуска значение " **автоматически**".

- Проверяет поддержку ссылок на веб-сайт для NETLOGON и SYSvol.

- Проверяет согласованность связи сайтов по имени узла и IP-адресу.

## <a name="syntax"></a>Синтаксис

```
dfsdiag /testdcs [/domain:<domain_name>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| /Domain`<domain_name>` | Имя проверяемого домена. Это необязательный параметр. Значение по умолчанию — локальный домен, к которому присоединен локальный узел. |

## <a name="examples"></a>Примеры

Чтобы проверить конфигурацию контроллеров домена в домене *contoso.com* , введите:

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда дфсдиаг](dfsdiag.md)
