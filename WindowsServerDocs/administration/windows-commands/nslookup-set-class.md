---
title: nslookup set class
description: Справочная статья по команде nslookup set Class, которая изменяет класс запроса.
ms.topic: reference
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 676c9dad9d01c6889ec472d68df831ba3eec15c7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038785"
---
# <a name="nslookup-set-class"></a>nslookup set class

Изменяет класс запроса. Класс указывает группу протоколов сведений.

## <a name="syntax"></a>Синтаксис

```
set class=<class>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<class>` | Допустимые значения:<ul><li>**В:** Указывает класс Интернета. Это значение по умолчанию.</li><li>**Chaos:** Указывает класс Chaos.</li><li>**Хесиод:** Указывает класс MIT Афина Хесиод.</li><li>**Все:** Задает использование любого из приведенных выше значений.</li></ul> |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
