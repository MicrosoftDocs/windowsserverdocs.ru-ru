---
title: ksetup addhosttorealmmap
description: Справочная статья по команде ksetup аддхосттореалммап, которая добавляет сопоставление имени участника-службы (SPN) между указанным узлом и областью.
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9722560a9ddebd01120dd60661ec895771ff9c6b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888144"
---
# <a name="ksetup-addhosttorealmmap"></a>ksetup addhosttorealmmap

Добавляет сопоставление имени участника-службы (SPN) между указанным узлом и областью. Эта команда также позволяет сопоставлять узел или несколько узлов, совместно использующих один и тот же DNS-суффикс к области.

Сопоставление сохраняется в реестре в разделе **HKEY_LOCAL_MACHINE \систем\куррентконтолсет\лса\керберос\хосттореалм**.

## <a name="syntax"></a>Синтаксис

```
ksetup /addhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- |------------ |
| `<hostname>` | Имя узла — это имя компьютера, оно может быть указано в качестве полного доменного имени компьютера. |
| `<realmname>` | Имя области указывается как DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. |

### <a name="examples"></a>Примеры

Чтобы подключить главный компьютер *IPops897* к сфере *contoso* , введите:

```
ksetup /addhosttorealmmap IPops897 CONTOSO
```

Проверьте реестр, чтобы убедиться, что сопоставление выполнено должным образом.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup делхосттореалммап, команда](ksetup-delhosttorealmmap.md)
