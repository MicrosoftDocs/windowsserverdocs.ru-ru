---
title: bitsadmin getpeercachingflags
description: Справочная статья по команде битсадмин жетпиркачингфлагс, которая получает флаги, определяющие, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также, если служба BITS может скачивать содержимое для задания с равноправных узлов.
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae22862c91fc9911bbf202dd51e52578b410995b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894028"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Получает флаги, которые определяют, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также, если служба BITS может скачивать содержимое для задания с одноранговых узлов.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить флаги для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getpeercachingflags myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
