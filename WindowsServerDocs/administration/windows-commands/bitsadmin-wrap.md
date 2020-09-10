---
title: bitsadmin wrap
description: Справочная статья по команде битсадмин Wrap, которая заключает в оболочку любую строку выходного текста, выходящего за пределы крайнего правого края окна команд, на следующую строку.
ms.topic: reference
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 24fa50e153d52ec74ab728a132aadd1b95c7a9da
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630382"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Заключает строку выходного текста, выходящего за пределы крайнего правого края окна команд, на следующую строку. Этот параметр необходимо указать перед любыми другими параметрами.

По умолчанию все коммутаторы, кроме коммутатора [монитора битсадмин](bitsadmin-monitor.md) , заключают выходной текст в оболочку.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ---------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Для получения сведений о задании с именем *мидовнлоаджоб* и обертывания выходного текста:

```
bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
