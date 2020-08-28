---
title: bitsadmin getclientcertificate
description: Справочная статья по команде битсадмин жетклиентцертификате, которая получает сертификат клиента из задания.
ms.topic: reference
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a2fe63369aab098b012462e063518463047218d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027832"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

Получает сертификат клиента из задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
