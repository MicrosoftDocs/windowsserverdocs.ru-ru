---
title: ftp user
description: Справочная статья по команде FTP User, которая указывает пользователя на удаленном компьютере.
ms.topic: reference
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ab95e8483767cbe24575b564dc0b315121ff241f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817258"
---
# <a name="ftp-user"></a>ftp user

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Указывает пользователя для удаленного компьютера.

## <a name="syntax"></a>Синтаксис

```
user <username> [<password>] [<account>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<username>` | Указывает имя пользователя для входа на удаленный компьютер. |
| `[<password>]` | Указывает пароль для *имени пользователя*. Если пароль не указан, но является обязательным, команда **FTP** запрашивает пароль. |
| `[<account>]` | Указывает учетную запись для входа на удаленный компьютер. Если *учетная запись* не указана, но является обязательной, команда **FTP** запрашивает учетную запись. |

### <a name="examples"></a>Примеры

Чтобы указать *Пользователь1* с паролем *password1*, введите:

```
user User1 Password1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
