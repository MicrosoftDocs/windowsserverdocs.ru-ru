---
title: ftp cd
description: Справочная статья по команде FTP CD, которая изменяет рабочий каталог на удаленном компьютере.
ms.topic: reference
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1acb7eb19c79a2574d901c400de58793350a6878
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101817849"
---
# <a name="ftp-cd"></a>ftp cd

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет рабочий каталог на удаленном компьютере.

## <a name="syntax"></a>Синтаксис

```
cd <remotedirectory>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| <remotedirectory> | Указывает каталог на удаленном компьютере, который необходимо изменить. |

### <a name="examples"></a>Примеры

Чтобы изменить каталог на удаленном компьютере на *документы*, введите:

```
cd Docs
```

Чтобы изменить каталог на удаленном компьютере на *возможные видеоролики*, введите:

```
cd  May Videos
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
