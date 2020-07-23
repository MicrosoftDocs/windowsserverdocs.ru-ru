---
title: ftp user
description: Справочная статья по команде FTP User, которая указывает пользователя на удаленном компьютере.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a77bfeb-27a9-4f2f-a3c4-2fef529fb569
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b1eea449765b58461d410f0e015d4978c3ad016
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957357"
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
