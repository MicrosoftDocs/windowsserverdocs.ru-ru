---
title: ksetup changepassword
description: Справочная статья по команде ksetup ChangePassword, которая использует центр распространения ключей (KDC) Password (кпассвд) для изменения пароля вошедшего в систему пользователя.
ms.topic: reference
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ca9a5a9b54c1608226a16113a8310473d59d6c0b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101815520"
---
# <a name="ksetup-changepassword"></a>ksetup changepassword

Использует значение пароля центр распространения ключей (KDC) (кпассвд) для изменения пароля вошедшего в систему пользователя. Выходные данные команды уведомляют о состоянии успешного выполнения или сбоя.

Проверить, задан ли **кпассвд** , можно, выполнив `ksetup /dumpstate` команду и просмотрев выходные данные.


## <a name="syntax"></a>Синтаксис

```
ksetup /changepassword <oldpassword> <newpassword>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<oldpassword>` | Указывает существующий пароль пользователя, вошедшего в систему. |
| `<newpassword>` | Указывает новый пароль пользователя, вошедшего в систему. Этот пароль должен соответствовать всем требованиям к паролю, установленным на этом компьютере. |

#### <a name="remarks"></a>Комментарии

- Если учетная запись пользователя не найдена в текущем домене, система предложит указать имя домена, в котором находится учетная запись пользователя.

- Если вы хотите принудительно сменить пароль при следующем входе в систему, эта команда позволяет использовать звездочку (*), поэтому пользователю будет предложено ввести новый пароль.

-

### <a name="examples"></a>Примеры

Чтобы изменить пароль пользователя, который в данный момент вошел в систему этого компьютера в этом домене, введите:

```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```

Чтобы изменить пароль пользователя, который в данный момент вошел в домен contoso, введите:

```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```

Чтобы заставить текущего пользователя изменить пароль при следующем входе в систему, введите:

```
ksetup /changepassword Pas$w0rd *
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup думпстате, команда](ksetup-dumpstate.md)

- [ksetup аддкпассвд, команда](ksetup-addkpasswd.md)

- [ksetup делкпассвд, команда](ksetup-delkpasswd.md)

- [ksetup думпстате, команда](ksetup-dumpstate.md)
