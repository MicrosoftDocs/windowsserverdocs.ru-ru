---
title: bitsadmin setdescription
description: Справочная статья по команде битсадмин SetDescription, которая задает описание указанного задания.
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d499b152f5cb3a846cc1de6ec65f07903421cf49
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893172"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

Задает описание для указанного задания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| description | Текст, используемый для описания задания. |

## <a name="examples"></a>Примеры

Чтобы получить описание задания с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
