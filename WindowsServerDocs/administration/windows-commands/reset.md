---
title: сброс
description: Справочная статья по команде Reset, которая сбрасывает DiskShadow.exe в состояние по умолчанию.
ms.topic: reference
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3bfa11742d6778089363ff7257e739eebb5b9838
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806907"
---
# <a name="reset"></a>сброс

Сбрасывает DiskShadow.exe в состояние по умолчанию. Эта команда особенно полезна при разделении составных операций DiskShadow, таких как **Создание**, **Импорт**, **резервное копирование** или **Восстановление**.

> [! ВАЖНО. После выполнения этой команды сведения о состоянии будут потеряны из команд, таких как **Add**, **Set**, **Load** или **Writer**. Эта команда также освобождает интерфейсы Ивссбаккупкомпонент и теряет непостоянные теневые копии.

## <a name="syntax"></a>Синтаксис

```
reset
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [создать команду](create.md)

- [Команда "Импорт"](import_1.md)

- [Backup, команда](begin-backup.md)

- [команда Restore](begin-restore.md)

- [добавить команду](add.md)

- [команда Set](set_2.md)

- [Команда Load](reg-load.md)

- [Writer, команда](writer.md)
