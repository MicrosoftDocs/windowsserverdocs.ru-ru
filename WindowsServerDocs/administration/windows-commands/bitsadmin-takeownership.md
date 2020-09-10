---
title: bitsadmin takeownership
description: Справочная статья по команде битсадмин такеовнершип, которая позволяет пользователю с правами администратора становиться владельцем указанного задания.
ms.topic: reference
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a4998ce3c28c839bb035a04c5472aae7c98b4eac
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630577"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

Позволяет пользователю с правами администратора становиться владельцем указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ---------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы стать владельцем задания с именем *мидовнлоаджоб*, сделайте следующее:

```
bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
