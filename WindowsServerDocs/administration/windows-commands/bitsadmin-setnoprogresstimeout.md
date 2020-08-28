---
title: bitsadmin setnoprogresstimeout
description: Справочная статья по команде битсадмин сетнопрогресстимеаут, которая задает время в секундах, в течение которого служба пытается переместить файл после возникновения временной ошибки.
ms.topic: reference
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc2559a963900234fd3111edb1a32e3f13b27e40
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027802"
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

### <a name="remarks"></a>Remarks

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
