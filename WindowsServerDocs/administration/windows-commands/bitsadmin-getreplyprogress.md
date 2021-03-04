---
title: bitsadmin getreplyprogress
description: Справочная статья по команде битсадмин жетреплипрогресс, которая получает размер и ход выполнения отправки и ответа сервера.
ms.topic: reference
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a932f881ef79c5915e390c087399e87aa213b5f5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821638"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

Возвращает размер и ход выполнения отправки и ответа сервера.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getreplyprogress <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить сведения о ходе отправки и ответа для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getreplyprogress myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
