---
title: dfsdiag
description: Справочная статья по команде дфсдиаг, которая предоставляет диагностические сведения для пространств имен DFS.
ms.topic: reference
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1edf5bc387a424a83162c93bc4d9036ffddb72c6
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818818"
---
# <a name="dfsdiag"></a>dfsdiag

Предоставляет диагностические сведения для пространств имен DFS.

## <a name="syntax"></a>Синтаксис

```
dfsdiag /testdcs [/domain:<domain name>]
dfsdiag /testsites </machine:<server name>| /DFSPath:<namespace root or DFS folder> [/recurse]> [/full]
dfsdiag /testdfsconfig /DFSRoot:<namespace>
dfsdiag /testdfsintegrity /DFSRoot:<DFS root path> [/recurse] [/full]
dfsdiag /testreferral /DFSpath:<DFS path to get referrals> [/full]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| [dfsdiag testdcs](dfsdiag-testdcs.md) | Проверяет конфигурацию контроллера домена. |
| [dfsdiag testsites](dfsdiag-testsites.md) | Проверяет связи сайтов. |
| [dfsdiag testdfsconfig](dfsdiag-testdfsconfig.md) | Проверяет конфигурацию пространства имен DFS. |
| [dfsdiag testdfsintegrity](dfsdiag-testdfsintegrity.md) | Проверяет целостность пространства имен DFS. |
| [dfsdiag testreferral](dfsdiag-testreferral.md) | Проверяет ответы на ссылки. |
| /? | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
