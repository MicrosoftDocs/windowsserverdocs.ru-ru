---
title: кэш битсадмин и Делетеурл
description: Справочная статья по битсадмин кэшу и команде Делетеурл, которая удаляет все записи кэша для данного URL-адреса.
ms.topic: reference
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6e1c3af4cfbb6c1ef21a86ead6d3975bf1f44cf6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632624"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>кэш битсадмин и Делетеурл

Удаляет все записи кэша для заданного URL-адреса.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /deleteURL URL
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| URL-адрес | Универсальный указатель ресурсов, определяющий удаленный файл. |

## <a name="examples"></a>Примеры

Удаление всех записей кэша для `https://www.contoso.com/en/us/default.aspx` :

```
bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда кэша битсадмин](bitsadmin-cache.md)
