---
title: Выбор схемы BranchCache
description: Узнайте, как узнать о режимах BranchCache и выбрать оптимальные режимы развертывания.
ms.topic: how-to
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: jgerend
author: JasonGerend
ms.date: 01/05/2021
ms.openlocfilehash: d8d5222ebcd38ddb1a1e68c99ef6cba81ce1ebb4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829313"
---
# <a name="choosing-a-branchcache-design"></a>Выбор схемы BranchCache

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела можно узнать о режимах BranchCache и выбрать оптимальные режимы развертывания.

Это руководством можно использовать для развертывания BranchCache в следующих режимах и сочетаниях режимов.

-   Все офисы филиалов настроены для режима распределенного кэша.

-   Все офисы филиалов настроены для режима размещенного кэша и имеют сервер размещенного кэша на сайте.

-   Некоторые офисы филиалов настроены для режима распределенного кэша, а некоторые офисы филиалов имеют сервер кэширования на сайте и настроены для режима размещенного кэша.

На следующем рисунке показана установка в двойном режиме с одним офисом филиала, настроенным для режима распределенного кэша, и одним филиалом, настроенным для режима размещенного кэша.

![Выбор схемы BranchCache](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)

Перед развертыванием BranchCache выберите предпочтительный режим для каждого офиса филиала в Организации.



