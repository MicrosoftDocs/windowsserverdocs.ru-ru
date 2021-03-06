---
title: ksetup mapuser
description: Справочная статья по команде ksetup мапусер, которая сопоставляет имя участника Kerberos с учетной записью.
ms.topic: reference
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 165eacddc989a37cbb9873c541aa93d17e743cba
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814905"
---
# <a name="ksetup-mapuser"></a>ksetup mapuser

Сопоставляет имя участника Kerberos с учетной записью.

## <a name="syntax"></a>Синтаксис

```
ksetup /mapuser <principal> <account>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<principal>` | Указывает полное доменное имя любого основного пользователя. Например, mike@corp.CONTOSO.COM. Если параметр учетной записи не указан, сопоставление удаляется для указанного участника. |
| `<account>` | Указывает любую учетную запись или имя группы безопасности, которая существует на этом компьютере, например **гость**, **Пользователи домена** или **Администратор**. Если этот параметр пропущен, сопоставление удаляется для указанного участника. |

#### <a name="remarks"></a>Комментарии

- Учетную запись можно определить отдельно, например, в качестве **гостей домена**, или можно использовать подстановочный знак (*) для включения всех учетных записей.

- Компьютер проверяет подлинность только субъектов данной области, если они представляют действительные билеты Kerberos.

- При каждом внесении изменений во внешний центр распространения ключей (KDC) и конфигурации сферы требуется перезагрузка компьютера, на котором был изменен параметр.

### <a name="examples"></a>Примеры

Чтобы просмотреть текущие сопоставленные параметры и область по умолчанию, введите:

```
ksetup
```

Чтобы связать учетную запись Mike Данселио в сфере Kerberos CONTOSO с учетной записью гостя на этом компьютере, предоставляя ей все права члена встроенной гостевой учетной записи без необходимости проверки подлинности на этом компьютере, введите:

```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```

Чтобы удалить сопоставление учетной записи Mike Данселио с учетной записью гостя на этом компьютере, чтобы предотвратить проверку подлинности на этом компьютере с учетными данными компании CONTOSO, введите:

```
ksetup /mapuser mike@corp.CONTOSO.COM
```

Чтобы связать учетную запись Mike Данселио в сфере Kerberos CONTOSO с любой существующей учетной записью на этом компьютере, введите:

```
ksetup /mapuser mike@corp.CONTOSO.COM *
```

> [!NOTE]
> Если на этом компьютере активны только стандартные учетные записи пользователя и гостя, то привилегиям Mike присваивается значение.

Чтобы связать все учетные записи в сфере Kerberos CONTOSO с любой существующей учетной записью с тем же именем на этом компьютере, введите:

```
ksetup /mapuser * *
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)
