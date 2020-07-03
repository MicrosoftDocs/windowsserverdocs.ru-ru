---
title: dfsdiag testdfsintegrity
description: Справочная статья по команде дфсдиаг тестдфсинтегрити, которая проверяет целостность пространства имен распределенная файловая система (DFS).
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7896174bb58c957e4c24b1c3f7e1b2bacc9f95f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930628"
---
# <a name="dfsdiag-testdfsintegrity"></a>dfsdiag testdfsintegrity

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Проверяет целостность пространства имен распределенная файловая система (DFS), выполняя следующие тесты:

- Проверяет наличие повреждений метаданных DFS или несоответствий между контроллерами домена.

- Проверяет конфигурацию перечисления на основе доступа, чтобы убедиться, что она согласована между метаданными DFS и общим ресурсом сервера пространства имен.

- Обнаруживает перекрывающиеся папки DFS (ссылки), дублирующиеся папки и папки с перекрывающимися целевыми объектами папок.

## <a name="syntax"></a>Синтаксис

```
dfsdiag /testdfsintegrity /DFSroot: <DFS root path> [/recurse] [/full]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /Дфсрут:`<DFS root path>` | Пространство имен DFS для диагностики. |
| /Recurse | Выполняет тестирование, включая взаимосвязи пространств имен. |
| /Full | Проверяет согласованность общего ресурса и списков ACL NTFS вместе с конфигурацией на стороне клиента для всех целевых объектов папки. Он также проверяет, задано ли свойство Online. |

## <a name="examples"></a>Примеры

Чтобы проверить целостность и согласованность пространств имен распределенная файловая система (DFS) в *contoso. ком\минамеспаце*, включая связи, введите:

```
dfsdiag /testdfsintegrity /DFSRoot:\contoso.com\MyNamespace /recurse /full
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда дфсдиаг](dfsdiag.md)
