---
title: ftp cd
description: Справочная статья по команде FTP CD, которая изменяет рабочий каталог на удаленном компьютере.
ms.topic: reference
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ab8992bfcbd10d487b5a460ecd25a0dad349ffc
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037312"
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
