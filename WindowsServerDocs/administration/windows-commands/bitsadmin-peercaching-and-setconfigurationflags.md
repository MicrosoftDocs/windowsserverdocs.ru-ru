---
title: bitsadmin peercaching и getconfigurationflags
description: Справочная статья для команды битсадмин и сетконфигуратионфлагс, которая устанавливает флаги конфигурации, определяющие, может ли компьютер передавать содержимое одноранговым узлам, а также может ли он скачивать содержимое с одноранговых узлов.
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ed6f638766378a24bc06c488cb90703d05f9c05
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893583"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin peercaching и getconfigurationflags

Задает флаги конфигурации, которые определяют, может ли компьютер передавать содержимое одноранговым узлам, а также может ли он скачивать содержимое с одноранговых узлов.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /peercaching /setconfigurationflags <job> <value>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| value | Целое число без знака со следующей интерпретацией битов в двоичном представлении:<ul><li>Чтобы разрешить загрузку данных задания с однорангового узла, установите наименьший значащий бит.</li><li>Чтобы разрешить передачу данных задания одноранговым узлам, установите второй бит справа.</li></ul>|

## <a name="examples"></a>Примеры

Чтобы указать данные задания, которые будут скачаны с узлов для задания с именем *мидовнлоаджоб*:

```
bitsadmin /peercaching /setconfigurationflags myDownloadJob 1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)

- [Команда кэширования битсадмин](bitsadmin-peercaching.md)
