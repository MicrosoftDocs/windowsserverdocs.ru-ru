---
title: ftp prompt
description: Справочная статья по команде FTP Prompt, которая включает и выключает режим запроса.
ms.topic: reference
ms.assetid: 930df39b-45c4-4e0b-bfe2-1d1963be817a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c666ba7bca3b8c9bb5be11b385ee7445be116083
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817598"
---
# <a name="ftp-prompt"></a>ftp prompt

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает и выключает режим запроса. По умолчанию режим подсказки включен. Если включен режим подсказки, команда FTP запрашивает во время нескольких передач файлов, позволяя выборочно получать или хранить файлы.

> [!NOTE]
> Вы можете использовать команды [FTP mget](ftp-mget.md) и [FTP мпут](ftp-mput_1.md) для перемещения всех файлов при отключенном режиме запроса.

## <a name="syntax"></a>Синтаксис

```
prompt
```

### <a name="examples"></a>Примеры

Чтобы включить или отключить режим подсказки, введите:

```
prompt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
