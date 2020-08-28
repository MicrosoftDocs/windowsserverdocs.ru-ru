---
title: ftp delete
description: Справочная статья по команде FTP DELETE, которая удаляет файлы на удаленных компьютерах.
ms.topic: reference
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebf1a770144409dca91ddea0a18a85536e05b926
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038062"
---
# <a name="ftp-delete"></a>ftp delete

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет файлы на удаленных компьютерах.

## <a name="syntax"></a>Синтаксис

```
delete <remotefile>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<remotefile>` | Указывает файл для удаления. |

### <a name="examples"></a>Примеры

Чтобы удалить файл *test.txt* на удаленном компьютере, введите:

```
delete test.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Дополнительные рекомендации по FTP](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
