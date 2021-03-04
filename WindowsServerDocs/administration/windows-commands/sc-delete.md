---
title: sc.exe удалить
description: Справочная статья по команде sc.exe DELETE, которая удаляет подраздел службы из реестра.
ms.topic: reference
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bdc567122f45572fa28aed0e45e1a15fa1ff0599
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806537"
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
