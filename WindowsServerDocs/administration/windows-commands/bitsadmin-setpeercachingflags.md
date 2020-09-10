---
title: bitsadmin setpeercachingflags
description: Справочная статья по команде битсадмин сетпиркачингфлагс, которая устанавливает флаги, определяющие, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также может ли задание скачивать содержимое с одноранговых узлов.
ms.topic: reference
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 59784ef9220abf1954b611524ba48b006550c1cd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630729"
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
| value | Целое число без знака, включая:<ul><li>**1.** задание может скачивать содержимое с одноранговых узлов.</li><li>**2.** файлы задания могут кэшироваться и обслуживаться одноранговыми узлами.</li></ul> |

## <a name="examples"></a>Примеры

Чтобы разрешить заданию с именем *мидовнлоаджоб* скачивать содержимое с одноранговых узлов:

```
bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
