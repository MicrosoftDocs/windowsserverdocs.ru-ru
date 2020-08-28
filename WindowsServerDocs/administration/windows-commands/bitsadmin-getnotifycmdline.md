---
title: bitsadmin getnotifycmdline
description: Справочная статья по команде битсадмин жетнотификмдлине, которая получает команду командной строки, которая выполняется, когда задание завершает передачу данных.
ms.topic: reference
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d85ed3dc301aed9d79619a1bbc6e9dc835b2102a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033482"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

Получает команду командной строки, которая будет запускаться после завершения передачи данных указанным заданием.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Для получения команды командной строки, используемой службой при завершении задания с именем *мидовнлоаджоб* .

```
bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
