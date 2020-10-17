---
title: проверка
description: Справочная статья по команде Verify, которая сообщает средству командной строки о необходимости проверки правильности записанных файлов на диск.
ms.topic: reference
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8a7f01e4251711af113fa10fe8ba110c53727115
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156690"
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
