---
title: add alias
description: Справочная статья по команде добавления псевдонима, которая добавляет псевдонимы в среду псевдонима.
ms.topic: reference
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 938a3c58e72791c65bae4d3938b14aa5d298580b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101823908"
---
# <a name="add-alias"></a>add alias

Добавляет псевдонимы в среду псевдонима. Если используется без параметров, команда **Добавить псевдоним** отображает справку в командной строке. Псевдонимы сохраняются в файле метаданных и загружаются с помощью команды **Load Metadata** .

## <a name="syntax"></a>Синтаксис

```
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<aliasname>` | Указывает имя псевдонима. |
| `<aliasvalue>` | Задает значение псевдонима. |
| `? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы получить список всех теней, включая их псевдонимы, введите:

```
list shadows all
```

В следующем фрагменте показана теневая копия, которой назначен псевдоним по умолчанию *VSS_SHADOW_x*.

```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```

Чтобы назначить новый псевдоним с именем *System1* для этой теневой копии, введите:

```
add alias System1 %VSS_SHADOW_1%
```

Кроме того, псевдоним можно назначить с помощью идентификатора теневой копии:

```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда загрузки метаданных](load-metadata.md)
