---
title: bitsadmin setnotifyflags
description: Справочная статья по команде битсадмин сетнотифифлагс, которая задает флаги уведомления о событии для указанного задания.
ms.topic: reference
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 48eb165ecb32e53868f9636418437d66c56542c0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630776"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

Задает флаги уведомления о событии для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setnotifyflags <job> <notifyflags>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| нотифифлагс | Может включать один или несколько следующих флагов уведомлений, в том числе:<ul><li>**1.** создает событие, когда все файлы в задании были переданы.</li><li>**2.** создает событие при возникновении ошибки.</li><li>**3.** формирует событие, когда все файлы завершили перенос или при возникновении ошибки.</li><li>**4.** отключает уведомления.</li></ul> |

## <a name="examples"></a>Примеры

Чтобы установить флаги уведомления для создания события при возникновении ошибки, для задания с именем *мидовнлоаджоб*:

```
bitsadmin /setnotifyflags myDownloadJob 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
