---
title: bitsadmin getsecurityflags
description: Справочная статья по команде битсадмин жетсекуритифлагс, которая сообщает о флагах безопасности HTTP для перенаправления URL-адресов и проверках, выполняемых на сертификате сервера во время перемещения.
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec6b5f4a52f1ecbf40b9374dd96914d4334eaf07
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893862"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Сообщает о флагах безопасности HTTP для перенаправления URL-адресов и проверках, выполняемых на сертификате сервера во время перемещения.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить флаги безопасности из задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getsecurityflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
