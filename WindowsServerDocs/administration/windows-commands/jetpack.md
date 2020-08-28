---
title: jetpack
description: Справочная статья по команде Jetpack, которая сжимает службу Windows Internet Name Service (WINS) или базу данных протокола DHCP.
ms.topic: reference
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf2664c142a169982acc0d11c34a53aea193d030
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035422"
---
# <a name="jetpack"></a>jetpack

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Сжимает службу Windows Internet Name Service (WINS) или базу данных протокола DHCP. Рекомендуется сжимать базу данных WINS при приближении 30 МБ.

Jetpack.exe сжимает базу данных следующим образом:

1. Копирование сведений о базе данных во временный файл базы данных.

2. Удаление исходного файла базы данных: WINS или DHCP.

3. Переименовывает временные файлы базы данных в исходное имя файла.

## <a name="syntax"></a>Синтаксис

```
jetpack.exe <database_name> <temp_database_name>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ------- | -------- |
| `<database_name>` | Задает имя исходного файла базы данных. |
| `<temp_database_name>` | Задает имя временного файла базы данных, создаваемого jetpack.exe.<p>Примечание. Этот временный файл удаляется по завершении процесса сжатия. Чтобы эта команда работала правильно, необходимо убедиться, что имя временного файла уникально и файл с таким именем еще не существует. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Для сжатия базы данных WINS, где **tmp. mdb** является временной базой данных, а **WINS. mdb** — это база данных WINS, введите:

```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack Wins.mdb Tmp.mdb
NET start WINS
```

Для сжатия базы данных DHCP, где **tmp. mdb** является временной базой данных, а **DHCP. mdb** — это база данных DHCP, введите:

```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERVER
jetpack Dhcp.mdb Tmp.mdb
NET start DHCPSERVER
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
