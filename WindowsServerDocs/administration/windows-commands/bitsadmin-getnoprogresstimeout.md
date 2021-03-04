---
title: bitsadmin getnoprogresstimeout
description: Справочная статья по команде битсадмин жетнопрогресстимеаут, которая получает время в секундах, в течение которого служба будет пытаться переместить файл после временной ошибки.
ms.topic: reference
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0da9441a23556ac162c9bc18a039769b34c84a4f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821878"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

Возвращает продолжительность времени в секундах, в течение которого служба будет пытаться переместить файл после возникновения временной ошибки.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |

## <a name="examples"></a>Примеры

Чтобы получить значение времени ожидания выполнения для задания с именем *мидовнлоаджоб*:

```
bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
