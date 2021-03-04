---
title: проверка
description: Справочная статья по команде Verify, которая сообщает средству командной строки о необходимости проверки правильности записанных файлов на диск.
ms.topic: reference
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 094bb5ff906b5aea70ae3fa2cf1cea64429e8687
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804597"
---
# <a name="verify"></a>проверка

Указывает средству командной строки (cmd.exe), следует ли проверять правильность записанных файлов на диск.

## <a name="syntax"></a>Синтаксис

```
verify [on | off]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[on | off]` | Переключает параметр **проверки** на значение ON или OFF. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы отобразить текущую настройку **проверки** , введите:

```
verify
```

Чтобы включить параметр **проверить** , введите:

```
verify on
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
