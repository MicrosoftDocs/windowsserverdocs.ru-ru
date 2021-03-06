---
title: Dfsutil
description: Справочная статья по команде Dfsutil, которая управляет пространствами имен, серверами и клиентами DFS.
ms.topic: reference
ms.assetid: ef5093a4-0d24-4b21-9d04-59933ad98e2c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4e5b6347569f525cfb223c89e8fb08ea4361c44b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818788"
---
# <a name="dfsutil"></a>Dfsutil

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Команда Dfsutil управляет пространствами имен, серверами и клиентами DFS.

## <a name="functionality-available-in-powershell"></a>Функциональные возможности, доступные в PowerShell

Модуль PowerShell [дфсн](/powershell/module/dfsn/) предоставляет эквивалентные функции для следующих параметров Dfsutil.

| Параметр | Описание |
| --------- | ----------- |
| корневой | Отображает, создает, удаляет, импортирует и экспортирует корни пространства имен. |
| link | Отображает, создает, удаляет или перемещает папки (ссылки). |
| target | Отображает, создает, удаляет целевой объект папки или сервер пространства имен. |
| свойство; | Отображает или изменяет целевой объект папки или сервер пространства имен. |
| server | Отображает или изменяет конфигурацию пространства имен. |
| домен | Отображает все пространства имен на основе домена в домене. |

## <a name="functionality-available-only-in-dfsutil"></a>Функциональные возможности, доступные только в Dfsutil

Следующие функциональные возможности доступны только в качестве параметров Dfsutil:

| Параметр | Описание |
| --------- | ----------- |
| клиент | Отображает или изменяет сведения о клиенте или разделы реестра. |
| диагностик | Выполните диагностику или просмотрите дфсдирс/дфспас. |
| cache | Отображает или очищает кэш клиента. |

Чтобы получить дополнительные сведения о каждой из этих команд, откройте командную строку на сервере с установленными средствами управления пространствами имен DFS и введите `dfsutil client /?` , `dfsutil diag /?` или `dfsutil cache /?` .

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
