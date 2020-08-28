---
title: сброс
description: Справочная статья по команде Reset, которая сбрасывает DiskShadow.exe в состояние по умолчанию.
ms.topic: reference
ms.assetid: afbdab44-199c-4e11-884f-e96804965c21
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ca1b0574fae1e0d00bc1f2cbec17ff9572ed253
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038342"
---
# <a name="reset"></a>сброс

Сбрасывает DiskShadow.exe в состояние по умолчанию. Эта команда особенно полезна при разделении составных операций DiskShadow, таких как **Создание**, **Импорт**, **резервное копирование**или **Восстановление**.

> [! ВАЖНО. После выполнения этой команды сведения о состоянии будут потеряны из команд, таких как **Add**, **Set**, **Load**или **Writer**. Эта команда также освобождает интерфейсы Ивссбаккупкомпонент и теряет непостоянные теневые копии.

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
