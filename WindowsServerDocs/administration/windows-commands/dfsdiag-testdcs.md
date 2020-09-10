---
title: dfsdiag testdcs
description: Справочная статья по команде дфсдиаг тестдкс, которая проверяет конфигурацию контроллеров домена в указанном домене.
ms.topic: reference
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0c2796cc149d905abae56bb909d337862c5fd7f2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633851"
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

| Параметр | Описание |
| --------- | ----------- |
| /Domain`<domain_name>` | Имя проверяемого домена. Этот параметр является необязательным. Значение по умолчанию — локальный домен, к которому присоединен локальный узел. |

## <a name="examples"></a>Примеры

Чтобы проверить конфигурацию контроллеров домена в домене *contoso.com* , введите:

```
dfsdiag /testdcs /domain:contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда дфсдиаг](dfsdiag.md)
