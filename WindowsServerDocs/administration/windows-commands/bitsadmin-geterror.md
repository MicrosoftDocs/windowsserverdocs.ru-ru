---
title: bitsadmin geterror
description: Справочный раздел для команды битсадмин Error, которая получает подробные сведения об ошибке для указанного задания.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7275bb813ef65f304cf8111c5a1ee387b7528e5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718020"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Извлекает подробные сведения об ошибке для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить сведения об ошибке для задания с именем *мидовнлоаджоб*:

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
