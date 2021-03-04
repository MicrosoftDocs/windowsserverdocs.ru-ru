---
title: bitsadmin getclientcertificate
description: Справочная статья по команде битсадмин жетклиентцертификате, которая получает сертификат клиента из задания.
ms.topic: reference
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0c37495eba30e1af09f8ffc1b36fba740376ce46
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822208"
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
