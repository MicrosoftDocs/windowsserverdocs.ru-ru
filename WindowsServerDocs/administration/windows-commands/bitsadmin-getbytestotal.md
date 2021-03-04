---
title: bitsadmin getbytestotal
description: Справочная статья по команде битсадмин жетбитестотал, которая получает размер указанного задания.
ms.topic: reference
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 846b0abc4642b44ce0b69493207136625eb8414a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822258"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

Возвращает размер указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить размер задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
