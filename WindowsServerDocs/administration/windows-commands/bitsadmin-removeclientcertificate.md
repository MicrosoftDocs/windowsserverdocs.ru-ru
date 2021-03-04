---
title: bitsadmin removeclientcertificate
description: Справочная статья по команде битсадмин ремовеклиентцертификате, которая удаляет сертификат клиента из задания.
ms.topic: reference
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d98d9f24c30c3550056cd4c2a12a28781c89376f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821198"
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
