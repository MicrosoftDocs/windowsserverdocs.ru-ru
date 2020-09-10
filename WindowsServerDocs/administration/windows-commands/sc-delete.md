---
title: Sc.exe удалить
description: Узнайте, как отменить регистрацию служб с помощью служебной программы sc.exe
ms.topic: reference
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8ce9eb203fd9db68629ce5412836eb694eb67162
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637100"
---
# <a name="scexe-delete"></a>Sc.exe удалить

Удаляет подраздел службы из реестра. Если служба запущена или другой процесс имеет открытый обработчик, служба помечается для удаления.

В разделе [Примеры](#examples) показан принцип использования этой команды.

## <a name="syntax"></a>Синтаксис

```
sc.exe [<ServerName>] delete [<ServiceName>]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|\<ServerName>|Указывает имя удаленного сервера, на котором расположена служба. Имя должно использовать формат UNC (например, \\ \\ MyServer). Чтобы запустить SC.exe локально, пропустите этот параметр.|
|\<ServiceName>|Указывает имя службы, возвращенное операцией **жеткэйнаме** .|
|?|Отображение справки в командной строке.|

## <a name="remarks"></a>Примечания

Не рекомендуется использовать sc.exe для удаления встроенных служб операционной системы, таких как DHCP, DNS или службы IIS. Сведения об установке, удалении и перенастройке ролей операционной системы, служб и компонентов см. в разделе [Установка и удаление ролей, служб ролей или компонентов](/WindowsServerDocs/administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) .

## <a name="examples"></a>Примеры

Чтобы удалить подраздел Service **невсерв** из реестра на локальном компьютере, введите:
```
sc.exe delete newserv
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
