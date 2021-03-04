---
title: кэш битсадмин и Делетеурл
description: Справочная статья по битсадмин кэшу и команде Делетеурл, которая удаляет все записи кэша для данного URL-адреса.
ms.topic: reference
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 94d5e865c54076b9a19fa1b4394cf20cce080345
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822588"
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
