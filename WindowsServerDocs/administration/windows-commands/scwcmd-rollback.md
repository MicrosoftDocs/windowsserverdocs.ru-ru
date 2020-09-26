---
title: scwcmd rollback
description: Справочная статья по команде отката команду scwcmd, которая применяет последнюю доступную политику отката, а затем удаляет эту политику отката.
ms.topic: reference
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e8f50995131ca01ea2bb58ee9371b12d9ec9a917
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388914"
---
# <a name="scwcmd-rollback"></a>scwcmd rollback

> Область применения: Windows Server 2012 R2 и Windows Server 2012

Применяет последнюю доступную политику отката, а затем удаляет эту политику отката.

## <a name="syntax"></a>Синтаксис

```
scwcmd rollback /m:<computername> [/u:<username>] [/pw:<password>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /m`<computername>` | Указывает имя NetBIOS, DNS-имя или IP-адрес компьютера, на котором должна быть выполнена операция отката. |
| /u`<username>` | Указывает альтернативную учетную запись пользователя, используемую при удаленном откате. Значение по умолчанию — вошедший в систему пользователь. |
| пароль`<password>` | Указывает альтернативные учетные данные пользователя для использования при удаленном откате. Значение по умолчанию — вошедший в систему пользователь. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы выполнить откат политики безопасности на компьютере с IP-адресом *172.16.0.0*, введите:

```
scwcmd rollback /m:172.16.0.0
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда команду scwcmd Analyze](scwcmd-analyze.md)

- [команду scwcmd configure, команда](scwcmd-configure.md)

- [команду scwcmd Register, команда](scwcmd-register.md)

- [Команда преобразования команду scwcmd](scwcmd-transform.md)

- [Команда команду scwcmd view](scwcmd-view.md)