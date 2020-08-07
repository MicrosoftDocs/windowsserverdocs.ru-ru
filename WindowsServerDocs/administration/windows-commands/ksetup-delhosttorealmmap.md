---
title: ksetup delhosttorealmmap
description: Справочная статья по команде ksetup делхосттореалммап, которая удаляет сопоставление имени участника-службы (SPN) между указанным узлом и областью.
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 953a8d33a65bb9c5aafd4d549f762772bc059ba4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888002"
---
# <a name="ksetup-delhosttorealmmap"></a>ksetup delhosttorealmmap

Удаляет сопоставление имени участника-службы (SPN) между указанным узлом и областью. Эта команда также удаляет все сопоставления между узлом и областью (или несколькими узлами в сфере).

Сопоставление сохраняется в реестре в разделе `HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm` . После выполнения этой команды рекомендуется убедиться, что сопоставление отображается в реестре.

## <a name="syntax"></a>Синтаксис

```
ksetup /delhosttorealmmap <hostname> <realmname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<hostname>` | Указывает полное доменное имя компьютера. |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. |

### <a name="examples"></a>Примеры

Чтобы изменить конфигурацию сферы CONTOSO и удалить сопоставление главного компьютера IPops897 с областью, введите:

```
ksetup /delhosttorealmmap IPops897 CONTOSO
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup аддхосттореалммап, команда](ksetup-addhosttorealmmap.md)
