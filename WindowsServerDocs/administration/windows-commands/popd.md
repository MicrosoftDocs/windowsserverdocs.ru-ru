---
title: popd
description: Справочная статья по команде pnputil, которая изменяет текущий каталог на каталог, который был последним сохранен командой pushd.
ms.topic: reference
ms.assetid: 8a4c52d5-9fd1-4eac-9c0c-5767b25728ed
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 84f009bb2a636e9bf655fbbf9c93b5c97198e8a4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101808419"
---
# <a name="popd"></a>popd

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Команда **popd** изменяет текущий каталог на каталог, который был последним сохранен командой **pushd** .

Каждый раз, когда вы используете команду **pushd** , хранится один каталог для использования. Однако можно хранить несколько каталогов с помощью команды **pushd** многократно. Каталоги последовательно хранятся в виртуальном стеке, поэтому при однократном использовании команды **pushd** в нижней части стека помещается каталог, в котором используется команда. При повторном использовании команды второй каталог помещается поверх первого. Процесс повторяется каждый раз при использовании команды **pushd** .

При использовании команды **popd** каталог в верхней части стека удаляется, а текущий каталог изменяется на этот каталог. При повторном использовании команды **popd** происходит удаление следующего каталога в стеке. Если расширения команд включены, команда **popd** удаляет все назначения букв дисков, созданные командой **pushd** .

## <a name="syntax"></a>Синтаксис

```
popd
```

### <a name="parameters"></a>Параметры

| Параметр | Description |
|--|--|
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы изменить текущий каталог с того, в котором выполнялась пакетная программа, а затем изменить ее обратно, введите:

```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [pushd](pushd.md)
