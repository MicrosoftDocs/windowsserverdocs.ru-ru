---
title: bitsadmin create
description: Справочная статья по команде битсадмин Create, которая создает задание перемещения с заданным отображаемым именем.
ms.topic: reference
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9fc2a5613c147f36a291ee06773abee5eb246c82
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101822358"
---
# <a name="bitsadmin-create"></a>bitsadmin create

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает задание перемещения с заданным отображаемым именем.

> [!NOTE]
> Типы параметров **/upload** и **/уплоад-репли** не поддерживаются в битах 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /create [type] displayname
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ------- | -------- |
| type | Существует три типа заданий:<ul><li>**Обновление.** Передает данные с сервера в локальный файл.</li><li>**Дают.** Передает данные из локального файла на сервер.</li><li>**/уплоад-репли.** Передает данные из локального файла на сервер и получает ответный файл с сервера.</li></ul>Если этот параметр не задан, по умолчанию используется значение **/download** . |
| displayname | Отображаемое имя, назначенное только что созданному заданию. |

## <a name="examples"></a>Примеры

Чтобы создать задание загрузки с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда возобновления битсадмин](bitsadmin-resume.md)

- [Команда битсадмин](bitsadmin.md)
