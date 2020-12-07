---
title: mklink
description: Справочная статья по команде Mklink, которая создает символьную или жесткую связь в каталоге или файле.
ms.topic: reference
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd605283396757f1ef0de05d620583c895f71f1a
ms.sourcegitcommit: f18097c21e50a09aef2f1937f52608b0042ef0e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2020
ms.locfileid: "96755311"
---
# <a name="mklink"></a>mklink

Создает символьную или жесткую связь в каталоге или файле.

## <a name="syntax"></a>Синтаксис

```
mklink [[/d] | [/h] | [/j]] <link> <target>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /d | Создает символьную ссылку каталога. По умолчанию эта команда создает символьную ссылку на файл. |
| /h | Создает жесткую связь вместо символьной ссылки. |
| /j | Создает соединение с каталогом. |
| `<link>` | Указывает имя создаваемой символьной ссылки. |
| `<target>` | Указывает путь (относительный или абсолютный), на который ссылается Новая символьная ссылка. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы создать и удалить символическую ссылку с именем MyFolder из корневого каталога в каталог \Users\User1\Documents и жесткую связь с именем MyFile. file к файлу example. File, расположенному в каталоге, введите:

```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда del](del.md)

- [RD, команда](rd.md)

- [Новый элемент в Windows PowerShell](/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
