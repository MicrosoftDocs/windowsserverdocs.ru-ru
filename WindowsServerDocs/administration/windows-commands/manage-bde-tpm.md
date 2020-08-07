---
title: Управление — TPM BDE
description: Справочная статья по команде TPM Manage-bde, которая настраивает доверенный платформенный модуль (TPM) компьютера (TPM).
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5a41ccff889fc729ce812523d64b9404378d32c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886654"
---
# <a name="manage-bde-tpm"></a>Управление — TPM BDE

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Настраивает доверенный платформенный модуль (TPM) компьютера (TPM).

## <a name="syntax"></a>Синтаксис

```
manage-bde -tpm [-turnon] [-takeownership <ownerpassword>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| -Турнон | Включает и активирует доверенный платформенный модуль, позволяя задать пароль владельца доверенного платформенного модуля. Можно также использовать **-t** в качестве сокращенной версии этой команды. |
| -такеовнершип | Получает владение доверенным платформенным модулем, задавая пароль владельца. Можно также использовать параметр **-o** в качестве сокращенной версии этой команды. |
| `<ownerpassword>` | Представляет пароль владельца, указанный для доверенного платформенного модуля. |
| -ComputerName | Указывает, что manage-bde.exe будет использоваться для изменения защиты BitLocker на другом компьютере. Можно также использовать параметр **-CN** в качестве сокращенной версии этой команды. |
| `<name>` | Представляет имя компьютера, на котором необходимо изменить защиту BitLocker. Допустимые значения включают имя NetBIOS компьютера и IP-адрес компьютера. |
| -? или/? | Отображает краткую справку в командной строке. |
| -Help или-h | Отображает полную справку в командной строке. |

### <a name="examples"></a>Примеры

Чтобы включить доверенный платформенный модуль, введите:

```
manage-bde  tpm -turnon
```

Чтобы стать владельцем TPM и задать для пароля владельца значение *0wnerP@ss* , введите:

```
manage-bde  tpm  takeownership 0wnerP@ss
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Командлеты управления TPM для Windows PowerShell](/powershell/module/trustedplatformmodule/)

- [Команда Manage-bde](manage-bde.md)
