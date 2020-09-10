---
title: bitsadmin removeclientcertificate
description: Справочная статья по команде битсадмин ремовеклиентцертификате, которая удаляет сертификат клиента из задания.
ms.topic: reference
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f2c739c1e1b1b3ee31d592adfb17e363dde865bf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631163"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

Удаляет сертификат клиента из задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы удалить сертификат клиента из задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /removeclientcertificate myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
