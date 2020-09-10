---
title: dfsdiag testsites
description: Справочная статья по дфсдиаг тестситес, которая проверяет конфигурацию сайтов доменных служб Active Directory (AD DS) путем проверки того, что серверы, выполняющие роль серверов пространства имен или целевых объектов (ссылок), имеют одинаковые связи сайтов на всех контроллерах домена.
ms.topic: reference
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c4c1b2eb578245b3d5f1ece443a78e9c0c00372b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634325"
---
# <a name="dfsdiag-testsites"></a>dfsdiag testsites

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Проверяет конфигурацию сайтов доменных служб Active Directory (AD DS), убедившись, что серверы, действующие как серверы пространства имен или целевые объекты папки (ссылки), имеют одинаковые связи сайтов на всех контроллерах домена.

## <a name="syntax"></a>Синтаксис

```
dfsdiag /testsites </machine:<server name>| /DFSpath:<namespace root or DFS folder> [/recurse]> [/full]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `/machine:<server name>` | Имя сервера, на котором необходимо проверить связь сайта. |
| `/DFSpath:<namespace root or DFS folder>` | Корневая папка пространства имен или распределенная файловая система (DFS) (ссылка) с целевыми объектами, для которых необходимо проверить связь сайта. |
| /Recurse | Перечисляет и проверяет связи сайтов для всех целевых объектов папки в указанном корне пространства имен. |
| /Full | Проверяет, что AD DS и реестр сервера содержат одинаковые сведения о взаимосвязи сайтов. |

## <a name="examples"></a>Примеры

Чтобы проверить связи сайтов в *мачине\мисервер*, введите:

```
dfsdiag /testsites /machine:MyServer
```

Чтобы проверить папку распределенная файловая система (DFS), чтобы проверить связь сайта, а также убедиться, что AD DS и реестр сервера содержат одинаковые сведения о связи сайта, введите:

```
dfsdiag /TestSites /DFSpath:\\contoso.com\namespace1\folder1 /full
```

Чтобы проверить корень пространства имен для проверки связи сайта, а также перечисления и проверки связей сайтов для всех целевых объектов папки в указанном корне пространства имен, а также проверки того, что AD DS и реестр сервера содержат одинаковые сведения о связи сайта, введите:

```
dfsdiag /testsites /DFSpath:\\contoso.com\namespace2 /recurse /full
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда дфсдиаг](dfsdiag.md)
