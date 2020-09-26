---
title: sc.exe удалить
description: Справочная статья по команде sc.exe DELETE, которая удаляет подраздел службы из реестра.
ms.topic: reference
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 12c09bd72259a8e4b58f134ca19f1fc825f2f1bb
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388465"
---
# <a name="scexe-delete"></a>sc.exe удалить

Удаляет подраздел службы из реестра. Если служба запущена или другой процесс имеет открытый обработчик, служба помечается для удаления.

> [!NOTE]
> Мы не рекомендуем использовать эту команду для удаления встроенных служб операционной системы, таких как DHCP, DNS или службы IIS. Сведения об установке, удалении и перенастройке ролей операционной системы, служб и компонентов см. в разделе [Установка и удаление ролей, служб ролей или компонентов](/WindowsServerDocs/administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) .

## <a name="syntax"></a>Синтаксис

```
sc.exe [<servername>] delete [<servicename>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<servername>` | Указывает имя удаленного сервера, на котором расположена служба. Имя должно использовать формат UNC (например, \\ MyServer). Чтобы запустить SC.exe локально, не используйте этот параметр. |
| `<servicename>` | Указывает имя службы, возвращенное операцией **жеткэйнаме** . |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы удалить подраздел Service **невсерв** из реестра на локальном компьютере, введите:

```
sc.exe delete NewServ
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
