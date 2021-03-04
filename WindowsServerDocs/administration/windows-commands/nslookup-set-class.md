---
title: nslookup set class
description: Справочная статья по команде nslookup set Class, которая изменяет класс запроса.
ms.topic: reference
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6de0c21e72a2bb1712c62052d18d1440473fd3f2
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101810087"
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
