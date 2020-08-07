---
title: lpq
description: Справочная статья по команде lpq, которая отображает состояние очереди печати на компьютере, на котором запущена управляющая программа командной строки (LPD).
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 550e94455ed7c57e723edb6608c42820e81fba0b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887062"
---
# <a name="lpq"></a>lpq

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает состояние очереди печати на компьютере, на котором запущена управляющая программа LPR.

## <a name="syntax"></a>Синтаксис

```
lpq -S <servername> -P <printername> [-l]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| -S`<servername>` | Указывает (по имени или IP-адресу) устройство общего доступа к компьютеру или принтеру, на котором размещена очередь печати LPD, с состоянием, которое необходимо отобразить. Этот параметр является обязательным и должен быть прописным. |
| -P`<Printername>` | Указывает (по имени) принтер для очереди печати с состоянием, которое необходимо отобразить. Этот параметр является обязательным и должен быть прописным. |
| -l | Указывает, что необходимо отобразить сведения о состоянии очереди печати. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы отобразить состояние очереди печати *Laserprinter1* на узле LPD в *10.0.0.45*, введите:

```
lpq -S 10.0.0.45 -P Laserprinter1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам системы печати](print-command-reference.md)
