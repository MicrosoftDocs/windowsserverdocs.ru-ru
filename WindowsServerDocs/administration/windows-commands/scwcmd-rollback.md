---
title: scwcmd rollback
description: Справочная статья по команде отката команду scwcmd, которая применяет последнюю доступную политику отката, а затем удаляет эту политику отката.
ms.topic: reference
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fc4fe285a3ede026a76fafc72b708326d84afdb1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806327"
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