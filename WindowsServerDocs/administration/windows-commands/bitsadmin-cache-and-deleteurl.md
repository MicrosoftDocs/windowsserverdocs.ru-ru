---
title: кэш битсадмин и Делетеурл
description: Справочная статья по битсадмин кэшу и команде Делетеурл, которая удаляет все записи кэша для данного URL-адреса.
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1a21a1994711e2548e9e08094f88f46edafe481
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894833"
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
