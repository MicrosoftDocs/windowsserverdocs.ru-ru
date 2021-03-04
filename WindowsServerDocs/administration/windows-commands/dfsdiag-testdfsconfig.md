---
title: dfsdiag testdfsconfig
description: Справочная статья по дфсдиаг тестдфсконфиг, которая проверяет конфигурацию пространства имен распределенная файловая система (DFS).
ms.topic: reference
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: badf202da56f4a0cad677df587c75f1da3ad17f5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818908"
---
# <a name="dfsdiag-testdfsconfig"></a>dfsdiag testdfsconfig

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Проверяет конфигурацию пространства имен распределенная файловая система (DFS), выполняя следующие действия.

- Проверяет, что служба пространства имен DFS запущена и для нее задан тип запуска **автоматически** на всех серверах пространства имен.

- Проверяет, является ли конфигурация реестра DFS согласованной между серверами пространства имен.

- Проверяет следующие зависимости на серверах кластеризованного пространства имен:

  - Зависимость корневого ресурса пространства имен от ресурса сетевого имени.

  - Зависимость ресурса сетевого имени от ресурса IP-адреса.

  - Зависимость корневого ресурса пространства имен от ресурса физического диска.

## <a name="syntax"></a>Синтаксис

```
dfsdiag /testdfsconfig /DFSroot:<namespace>
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /Дфсрут:`<namespace>` | Пространство имен (корень DFS) для диагностики. |

## <a name="examples"></a>Примеры

Чтобы проверить конфигурацию пространств имен распределенная файловая система (DFS) в *contoso. ком\минамеспаце*, введите:

```
dfsdiag /testdfsconfig /DFSroot:\contoso.com\MyNamespace
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда дфсдиаг](dfsdiag.md)
