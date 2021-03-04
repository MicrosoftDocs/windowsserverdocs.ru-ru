---
title: ftp ascii
description: Справочная статья по команде FTP ASCII, которая задает тип перемещения файла ASCII.
ms.topic: reference
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6f421deb198639893b0d2fb8dbacaf1eff6db54c
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817988"
---
# <a name="ftp-ascii"></a>ftp ascii

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Задает тип перемещения файла ASCII. Команда **FTP** поддерживает как ASCII (по умолчанию), так и двоичные типы передачи файлов изображений, но при передаче текстовых файлов рекомендуется использовать ASCII. В режиме ASCII выполняется преобразование символов в стандартную сетевую кодировку и из нее. Например, символы конца строки при необходимости преобразуются в зависимости от целевой операционной системы.

## <a name="syntax"></a>Синтаксис

```
ascii
```

### <a name="examples"></a>Примеры

Чтобы задать тип перемещения файла ASCII, введите:

```
ascii
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Двоичная команда FTP](ftp-binary.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
