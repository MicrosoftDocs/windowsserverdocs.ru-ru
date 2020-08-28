---
title: bitsadmin setpeercachingflags
description: Справочная статья по команде битсадмин сетпиркачингфлагс, которая устанавливает флаги, определяющие, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также может ли задание скачивать содержимое с одноранговых узлов.
ms.topic: reference
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1305d8d865f51556f4b518c7972eaff4ca9ec3e5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026212"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

Устанавливает флаги, определяющие, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также может ли задание скачивать содержимое с одноранговых узлов.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| значение | Целое число без знака, включая:<ul><li>**1.** задание может скачивать содержимое с одноранговых узлов.</li><li>**2.** файлы задания могут кэшироваться и обслуживаться одноранговыми узлами.</li></ul> |

## <a name="examples"></a>Примеры

Чтобы разрешить заданию с именем *мидовнлоаджоб* скачивать содержимое с одноранговых узлов:

```
bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
