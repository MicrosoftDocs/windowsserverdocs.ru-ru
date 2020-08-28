---
title: sfc
description: Справочная статья для SFC, который сканирует и проверяет целостность всех защищенных системных файлов и заменяет неверные версии на правильные версии.
ms.topic: reference
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6aa1fd38eaab1ffe3d6c3b9f2e4913d6a1e0ca4d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024888"
---
# <a name="sfc"></a>sfc

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Проверяет целостность всех защищенных системных файлов и заменяет их правильными версиями.


## <a name="syntax"></a>Синтаксис
```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

#### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|/scannow|Проверяет целостность всех защищенных системных файлов и восстанавливает файлы с проблемами, когда это возможно.|
|/верифйонли|Проверяет целостность всех защищенных системных файлов. Операции восстановления не выполняются.|
|/сканфиле|Проверяет целостность указанного файла и восстанавливает файл, если это возможно.|
|\<file>|Указанный полный путь и имя файла|
|/верифифиле|проверяет целостность указанного файла. Операции восстановления не выполняются.|
|/оффвиндир|Указывает расположение автономного каталога Windows для восстановления в автономном режиме.|
|/оффбутдир|Указывает расположение автономного каталога загрузки для автономной работы|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Remarks
-   Для запуска **sfc.exe**необходимо войти в систему в качестве члена группы "Администраторы".
-   Если **sfc** обнаруживает, что защищенный файл был перезаписан, он извлекает правильную версию файла из папки **systemroot\system32\dllcache** , а затем заменяет неверный файл.
-   Между **sfc** в windows Server 2003, windows Server 2008 и windows Server 2008 R2 существуют функциональные различия:
-   Дополнительные сведения о **sfc** в Windows Server 2003 см. в [статье 310747](https://go.microsoft.com/fwlink/?LinkId=227069) в базе знаний Майкрософт.
-   Дополнительные сведения о **sfc** в windows Server 2008 и windows Server 2008 R2 см. в разделе [средство проверки системных файлов](https://go.microsoft.com/fwlink/?LinkId=227071).

## <a name="examples"></a>Примеры
Чтобы проверить ** файлkernel32.dll**, введите:
```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```
Чтобы настроить автономное восстановление файла **kernel32.dll** с автономной загрузочной папкой **d:** и автономным каталогом Windows, установленным в **d:\Windows**, введите:
```
sfc /scanfile=d:\windows\system32\kernel32.dll /offbootdir=d:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

