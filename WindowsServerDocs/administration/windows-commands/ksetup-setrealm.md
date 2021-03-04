---
title: ksetup setrealm
description: Справочная статья по команде ksetup сетреалм, которая задает имя области Kerberos.
ms.topic: reference
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 52ff1c8d8df2c4aa33cc76b5d1fa33a364be0679
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814625"
---
# <a name="ksetup-setrealm"></a>ksetup setrealm

Задает имя области Kerberos.

> [!IMPORTANT]
> Установка области Kerberos на контроллере домена не поддерживается. Попытка сделать это вызовет предупреждение и сбой команды.

## <a name="syntax"></a>Синтаксис

```
ksetup /setrealm <DNSdomainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<DNSdomainname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. Можно использовать полное доменное имя или простую форму имени. Если вы не используете прописные буквы в качестве DNS-имени, вам будет предложено выполнить проверку, чтобы продолжить. |

### <a name="examples"></a>Примеры

Чтобы задать для области этого компьютера определенное доменное имя и ограничить доступ неконтроллером домена только к сфере CONTOSO Kerberos, введите:

```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup removerealm](ksetup-removerealm.md)
