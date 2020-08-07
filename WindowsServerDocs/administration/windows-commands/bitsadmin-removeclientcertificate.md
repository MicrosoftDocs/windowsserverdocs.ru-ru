---
title: bitsadmin removeclientcertificate
description: Справочная статья по команде битсадмин ремовеклиентцертификате, которая удаляет сертификат клиента из задания.
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f4b2a17a08f3c2b224d90237975841644ea16ecd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893375"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate

Удаляет сертификат клиента из задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /removeclientcertificate <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
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
