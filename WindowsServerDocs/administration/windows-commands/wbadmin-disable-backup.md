---
title: wbadmin disable backup
description: Справочная статья по команде Wbadmin Disable Backup, которая останавливает выполнение запланированных ежедневных резервных копий.
ms.topic: reference
ms.assetid: 5176cbd9-0696-4b3f-9c35-272dd84f7898
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7cee06dc8b71f38cff333d2af9cc23453abc94bf
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804547"
---
# <a name="wbadmin-disable-backup"></a>wbadmin disable backup

Прекращает выполнение существующих запланированных ежедневных резервных копий.

Чтобы отключить запланированное ежедневное резервное копирование с помощью этой команды, необходимо быть членом группы " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши **командную строку** и выбрав команду **Запуск от имени администратора**.

## <a name="syntax"></a>Синтаксис

```
wbadmin disable backup [-quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -quiet | Выполняет команду без запроса пользователю. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Wbadmin](wbadmin.md)

- [Команда Wbadmin enable backup](wbadmin-enable-backup.md)