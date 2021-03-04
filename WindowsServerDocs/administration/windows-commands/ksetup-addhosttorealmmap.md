---
title: ksetup addhosttorealmmap
description: Справочная статья по команде ksetup аддхосттореалммап, которая добавляет сопоставление имени участника-службы (SPN) между указанным узлом и областью.
ms.topic: reference
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bdbc6b7b1a18e0c6db45dccfebc5e90c2aaa21b5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101815797"
---
# <a name="ksetup-addhosttorealmmap"></a>ksetup addhosttorealmmap

Добавляет сопоставление имени участника-службы (SPN) между указанным узлом и областью. Эта команда также позволяет сопоставлять узел или несколько узлов, совместно использующих один и тот же DNS-суффикс к области.

Сопоставление сохраняется в реестре в разделе **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**.

## <a name="syntax"></a>Синтаксис

```
ksetup /addhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
