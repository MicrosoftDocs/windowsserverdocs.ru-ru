---
title: ksetup delkdc
description: Справочная статья по команде ksetup делкдк, которая удаляет экземпляры имен центр распространения ключей (KDC) для области Kerberos.
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f57e409afc62b831590f371befee2775f5c9cce9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887970"
---
# <a name="ksetup-delkdc"></a>ksetup delkdc

Удаляет экземпляры имен центр распространения ключей (KDC) для области Kerberos.

Сопоставление сохраняется в реестре в разделе `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains` . После выполнения этой команды рекомендуется убедиться, что KDC был удален и больше не отображается в списке.

> [!NOTE]
> Чтобы удалить данные конфигурации сферы с нескольких компьютеров, используйте оснастку " **шаблон конфигурации безопасности** " с распределением политик, а не используйте команду **ksetup** явным образом на отдельных компьютерах.

## <a name="syntax"></a>Синтаксис

```
ksetup /delkdc <realmname> <KDCname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. Это область по умолчанию, которая отображается при выполнении команды **ksetup** и представляет собой область, из которой необходимо удалить KDC. |
| `<KDCname>` | Задает с учетом регистра полное доменное имя, например mitkdc.contoso.com. |

### <a name="examples"></a>Примеры

Чтобы просмотреть все связи между областью Windows и областью, отличной от Windows, и определить, какие из них нужно удалить, введите:

```
ksetup
```

Чтобы удалить связь, введите:

```
ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup аддкдк, команда](ksetup-addkdc.md)