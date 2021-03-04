---
title: bitsadmin getsecurityflags
description: Справочная статья по команде битсадмин жетсекуритифлагс, которая сообщает о флагах безопасности HTTP для перенаправления URL-адресов и проверках, выполняемых на сертификате сервера во время перемещения.
ms.topic: reference
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 356bcd690a3b8f656570c9a96a4438c0bcabd203
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821648"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Сообщает о флагах безопасности HTTP для перенаправления URL-адресов и проверках, выполняемых на сертификате сервера во время перемещения.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
