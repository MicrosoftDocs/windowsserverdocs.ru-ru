---
title: subst
description: Сведения о связывании пути с буквой диска.
ms.topic: article
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 385359a49ee1cc4df95a17bef6c2aed4704a2dcd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881950"
---
# <a name="subst"></a>subst



Связывает путь с буквой диска. При использовании без параметров **subst** отображает имена используемых виртуальных дисков.



## <a name="syntax"></a>Синтаксис

```
subst [<Drive1>: [<Drive2>:]<Path>]
subst <Drive1>: /d
```

### <a name="parameters"></a>Параметры

|Параметр|Описание:|
|---------|-----------|
|\<Drive1>:|Указывает виртуальный диск, которому необходимо назначить путь.|
|[\<Drive2>:]\<Path>|Указывает физический диск и путь, который вы хотите назначить виртуальному диску.|
|/d|Удаляет подставляемый (виртуальный) диск.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Remarks

-   Следующие команды не работают и не должны использоваться на дисках, указанных в команде **subst** :

    **chkdsk**

    **diskcomp**

    **diskcopy**

    **format**

    **label**

    **recover**
-   Параметр *диск1* должен находиться в диапазоне, указанном командой **ластдриве** . В противном случае **subst** выводит следующее сообщение об ошибке:

    `Invalid parameter - drive1:`

## <a name="examples"></a><a name="BKMK_examples"></a>Примеры

Чтобы создать виртуальный диск Z для пути Б:\усер\бетти\формс, введите:
```
subst z: b:\user\betty\forms
```
Вместо того чтобы вводить полный путь, можно получить доступ к этому каталогу, введя букву виртуального диска, а затем двоеточие, как показано ниже.
```
z:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)