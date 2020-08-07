---
title: bitsadmin getnoprogresstimeout
description: Справочная статья по команде битсадмин жетнопрогресстимеаут, которая получает время в секундах, в течение которого служба будет пытаться переместить файл после временной ошибки.
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0bd85d93416e5e5718f5be830c99936a3080e24
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894137"
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
