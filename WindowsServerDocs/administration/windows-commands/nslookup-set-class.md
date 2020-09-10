---
title: nslookup set class
description: Справочная статья по команде nslookup set Class, которая изменяет класс запроса.
ms.topic: reference
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5f4eb309c3972230247bf231b0e731e146d8159a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634029"
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
