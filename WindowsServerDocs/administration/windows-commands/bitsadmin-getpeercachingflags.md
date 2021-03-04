---
title: bitsadmin getpeercachingflags
description: Справочная статья по команде битсадмин жетпиркачингфлагс, которая получает флаги, определяющие, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также, если служба BITS может скачивать содержимое для задания с равноправных узлов.
ms.topic: reference
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b79e2a3b1b36be5dba2233489d15b0d460632dfa
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821818"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Получает флаги, которые определяют, могут ли файлы задания кэшироваться и обслуживаться одноранговым узлам, а также, если служба BITS может скачивать содержимое для задания с одноранговых узлов.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getpeercachingflags <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
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
