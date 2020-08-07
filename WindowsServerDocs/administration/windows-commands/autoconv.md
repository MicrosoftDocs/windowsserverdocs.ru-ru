---
title: autoconv
description: Справочная статья по команде аутоконв, которая преобразует тома FAT и FAT32 в файловую систему NTFS.
ms.topic: article
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f4c7ed1a2c370de46e02130fd06e1b9326207e9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895269"
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
