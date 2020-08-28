---
title: bitsadmin getreplyprogress
description: Справочная статья по команде битсадмин жетреплипрогресс, которая получает размер и ход выполнения отправки и ответа сервера.
ms.topic: reference
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80c227d8de0148236a975a3d11162c0c152e5f7a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034872"
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
