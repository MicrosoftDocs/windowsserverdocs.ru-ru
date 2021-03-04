---
title: sfc
description: Справочная статья по команде SFC, которая сканирует и проверяет целостность всех защищенных системных файлов и заменяет неверные версии на правильные версии.
ms.topic: reference
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 980f3949515f6b5799ce5b9a3de7f1fd47ad64ca
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805757"
---
# <a name="sfc"></a>sfc

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Проверяет целостность всех защищенных системных файлов и заменяет их правильными версиями. Если эта команда обнаруживает, что защищенный файл был перезаписан, он извлекает правильную версию файла из папки **systemroot\system32\dllcache** , а затем заменяет неверный файл.

> [!IMPORTANT]
> Для выполнения этой команды необходимо войти в систему в качестве члена группы "Администраторы".

## <a name="syntax"></a>Синтаксис

```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /scannow | Проверяет целостность всех защищенных системных файлов и восстанавливает файлы с проблемами, когда это возможно. |
| /верифйонли | Проверяет целостность всех защищенных системных файлов без выполнения восстановления. |
| /сканфиле `<file>` | Проверяет целостность указанного файла (полный путь и имя файла) и пытается устранить обнаруженные проблемы. |
| /верифифиле `<file>` | Проверяет целостность указанного файла (полный путь и имя файла) без выполнения восстановления. |
| /оффвиндир `<offline windows directory>` | Указывает расположение автономного каталога Windows для восстановления в автономном режиме. |
| /оффбутдир `<offline boot directory>` | Указывает расположение автономного каталога загрузки для автономного восстановления. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы проверить *файлkernel32.dll*, введите:

```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```

Чтобы настроить автономное восстановление файла *kernel32.dll* с каталогом автономной загрузки со значением * D: \* и автономным каталогом Windows, для которого задано значение *D:\Windows*, введите:

```
sfc /scanfile=D:\windows\system32\kernel32.dll /offbootdir=D:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
