---
title: subst
description: Справочная статья по команде subst, которая связывает путь с буквой диска.
ms.topic: reference
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 52d45c9139c70c4f513a972f7789f872145c8b63
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718231"
---
# <a name="subst"></a>subst

Связывает путь с буквой диска. При использовании без параметров **subst** отображает имена используемых виртуальных дисков.

## <a name="syntax"></a>Синтаксис

```
subst [<drive1>: [<drive2>:]<path>]
subst <drive1>: /d
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<drive1>:` | Указывает виртуальный диск, которому необходимо назначить путь. |
| `[<drive2>:]<path>` | Указывает физический диск и путь, который вы хотите назначить виртуальному диску. |
| /d | Удаляет подставляемый (виртуальный) диск. |
| /? | Отображение справки в командной строке. |

## <a name="remarks"></a>Комментарии

- Следующие команды не работают и не должны использоваться на дисках, указанных в команде **subst** :

  - [команда chkdsk](chkdsk.md)

    [команда diskcomp](diskcomp.md)

    [команда diskcopy](diskcopy.md)

    [Команда Format](format.md)

    [Метка, команда](label.md)

    [Команда Recover](recover.md)

- `<drive1>`Параметр должен находиться в диапазоне, указанном командой **ластдриве** . В противном случае **subst** выводит следующее сообщение об ошибке: `Invalid parameter - drive1:`

## <a name="examples"></a>Примеры

Чтобы создать виртуальный диск z для пути б:\усер\бетти\формс, введите:

```
subst z: b:\user\betty\forms
```

Вместо того чтобы вводить полный путь, можно получить доступ к этому каталогу, введя букву виртуального диска, а затем двоеточие, как показано ниже.

```
z:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)