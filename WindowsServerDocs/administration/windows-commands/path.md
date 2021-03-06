---
title: path
description: Справочная статья по настройке пути к команде в переменной среды PATH с указанием набора каталогов, используемых для поиска исполняемых файлов (exe).
ms.topic: reference
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 54a62b0e2da1dd21eb567bb59e20e194dcce2af7
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101808905"
---
# <a name="path"></a>path

Задает путь к команде в переменной среды PATH, указывающий набор каталогов, используемых для поиска исполняемых файлов (exe). При использовании без параметров эта команда отображает текущий путь к команде.

## <a name="syntax"></a>Синтаксис

```
path [[<drive>:]<path>[;...][;%PATH%]]
path ;
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[<drive>:]<path>` | Указывает диск и каталог, который нужно задать в пути к команде. Текущий каталог всегда ищется перед каталогами, указанными в пути к команде. |
| ; | Разделяет каталоги в пути команды. При использовании без параметров **;** очищает существующие пути к командам из переменной среды PATH и направляет Cmd.exe для поиска только в текущем каталоге. |
| `%PATH%` | Добавляет путь команды к существующему набору каталогов, перечисленных в переменной среды PATH. Если включить этот параметр, Cmd.exe заменит его значениями пути к командам, найденными в переменной среды PATH, что устраняет необходимость вручную вводить эти значения в командной строке. |
| /? | Отображение справки в командной строке. |

## <a name="remarks"></a>Комментарии


- Операционная система Windows выполняет поиск по расширениям имен файлов по умолчанию в следующем порядке приоритета: exe, com, bat и cmd. Это означает, что если вы ищете пакетный файл с именем, acct.bat, но у вас есть приложение с именем acct.exe в том же каталоге, необходимо включить расширение bat в командную строку.

- Если два или более файлов в пути команды имеют одинаковое имя файла и расширение, эта команда сначала выполняет поиск указанного имени файла в текущем каталоге. Затем он ищет каталоги в пути команды в том порядке, в котором они указаны в переменной среды PATH.

- При помещении команды **path** в файл AUTOEXEC. NT операционная система Windows автоматически добавляет указанный путь поиска подсистемы MS-DOS при каждом входе в систему. Cmd.exe не использует файл AUTOEXEC. NT. При запуске из ярлыка Cmd.exe наследует переменные среды, заданные в Мой компьютер/свойствах/дополнительном/окружении.

## <a name="examples"></a>Примеры

Для поиска по путям *к:\усер\таксес*, *б:\усер\инвест* и *б:\бин* для внешних команд введите:

```
path c:\user\taxes;b:\user\invest;b:\bin
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
