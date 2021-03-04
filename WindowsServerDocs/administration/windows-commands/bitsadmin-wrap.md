---
title: bitsadmin wrap
description: Справочная статья по команде битсадмин Wrap, которая заключает в оболочку любую строку выходного текста, выходящего за пределы крайнего правого края окна команд, на следующую строку.
ms.topic: reference
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c259a6f1102f2bfb5d4ed1e1de0e6c4a74cedb26
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820488"
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
