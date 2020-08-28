---
title: bitsadmin getnotifyflags
description: Справочная статья по команде битсадмин жетнотифифлагс, которая получает флаги уведомления для указанного задания.
ms.topic: reference
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b0281629eb98a7f74defb0971b691fd656d9d97
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033442"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

Получает флаги уведомления для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="remarks"></a>Remarks

Задание может содержать один или несколько следующих флагов уведомления:

| Flag | Описание |
| ----- | ----- |
| 0x001 | Создавать событие, когда все файлы в задании были переданы. |
| 0x002 | Создавать событие при возникновении ошибки. |
| 0x004 | Отключение уведомлений. |
| 0x008 | Создание события при изменении или переносе задания. |

## <a name="examples"></a>Примеры

Чтобы получить флаги уведомления для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
