---
title: bitsadmin getfilestotal
description: Справочная статья по команде битсадмин жетфилестотал, которая получает количество файлов в указанном задании.
ms.topic: reference
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 37be96f1fa7605aca542735d37dbf4c5617282d8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822008"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

Извлекает количество файлов в указанном задании.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить количество файлов, включаемых в задание с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>См. также:

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
