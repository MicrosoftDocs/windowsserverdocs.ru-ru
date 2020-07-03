---
title: bitsadmin setnotifyflags
description: Справочная статья по команде битсадмин сетнотифифлагс, которая задает флаги уведомления о событии для указанного задания.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4054788bb8c14e4bd9be38296f5c0f933de9462
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927617"
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
