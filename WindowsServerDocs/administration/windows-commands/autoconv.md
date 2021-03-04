---
title: autoconv
description: Справочная статья по команде аутоконв, которая преобразует тома FAT и FAT32 в файловую систему NTFS.
ms.topic: reference
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6a3e9da89b45c4adbefc26c0c6965b00bf1b8b0f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101823048"
---
# <a name="autoconv"></a>autoconv

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Преобразует тома с файловой системой FAT и FAT32 в файловую систему NTFS, при этом существующие файлы и каталоги остаются без изменений при запуске после запуска **Autochk** . тома, преобразованные в файловую систему NTFS, не могут быть преобразованы обратно в FAT или FAT32.

> [!IMPORTANT]
> Невозможно запустить **аутоконв** из командной строки. Это может выполняться при запуске, если задано через **convert.exe**.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Autochk](autochk.md)

- [преобразовать команду](convert.md)
