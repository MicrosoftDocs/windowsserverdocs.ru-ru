---
title: bitsadmin setnoprogresstimeout
description: Справочная статья по команде битсадмин сетнопрогресстимеаут, которая задает время в секундах, в течение которого служба пытается переместить файл после возникновения временной ошибки.
ms.topic: reference
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0be9d662756dc318a4789f3f55dabdc13be7f5f2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101820848"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

Задает период времени в секундах, в течение которого BITS пытается переместить файл после первой временной ошибки.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setnoprogresstimeout <job> <timeoutvalue>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| тимеаутвалуе | Продолжительность времени, в течение которого служба BITS ожидает передачи файла после первой ошибки в секундах. |

### <a name="remarks"></a>Комментарии

- Интервал времени ожидания "не выполняется" начинается, когда задание сталкивается с первой временной ошибкой.

- Интервал времени ожидания останавливается или сбрасывается при успешном передаче байта данных.

- Если интервал времени ожидания "не выполнено" превышает значение *тимеаутвалуе*, задание помещается в неустранимую ошибку.

## <a name="examples"></a>Примеры

Чтобы установить значение времени ожидания "не выполняется" равным 20 секундам, для задания с именем *мидовнлоаджоб*:

```
bitsadmin /setnoprogresstimeout myDownloadJob 20
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
