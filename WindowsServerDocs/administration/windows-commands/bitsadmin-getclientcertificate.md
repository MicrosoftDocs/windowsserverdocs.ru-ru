---
title: bitsadmin getclientcertificate
description: Справочная статья по команде битсадмин жетклиентцертификате, которая получает сертификат клиента из задания.
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3deb42c0b29f238bfd0a3b0fddbea14833d38b4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894509"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

Получает сертификат клиента из задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить сертификат клиента для задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
