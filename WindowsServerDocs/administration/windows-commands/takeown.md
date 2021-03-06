---
title: takeown
description: Справочная статья по команде takeown, которая позволяет администратору восстановить доступ к файлу, который ранее был отклонен.
ms.topic: reference
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 83568ba954777c59a8623ec37cca05feb9de6a62
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805507"
---
# <a name="takeown"></a>takeown

Позволяет администратору восстановить доступ к файлу, который ранее был запрещен, путем предоставления администратору владельца файла. Эта команда обычно используется в пакетных файлах.

## <a name="syntax"></a>Синтаксис

```
takeown [/s <computer> [/u [<domain>\]<username> [/p [<password>]]]] /f <filename> [/a] [/r [/d {Y|N}]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| ключ `<computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте символы обратной косой черты). Значением по умолчанию является локальный компьютер. Этот параметр применяется ко всем файлам и папкам, указанным в команде. |
| /u `[<domain>\]<username>` | Запускает скрипт с разрешениями указанной учетной записи пользователя. По умолчанию используется значение системные разрешения. |
| /p `[<[password>]` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| /f `<filename>` | Указывает имя файла или шаблон имени каталога. При указании шаблона можно использовать подстановочный знак `*` . Также можно использовать синтаксис `<sharename>\<filename>` . |
| /a | Предоставляет права владения группе администраторов вместо текущего пользователя. Если этот параметр не указан, владение файлом назначается пользователю, который в данный момент вошел в систему компьютера. |
| /r | Выполняет рекурсивную операцию для всех файлов в указанном каталоге и подкаталогах. |
| /d `{Y | N}` | Подавляет запрос подтверждения, отображаемый, когда текущий пользователь не имеет разрешения на **список папок** в указанном каталоге, а использует указанное значение по умолчанию. Допустимые значения параметра **/d** :<ul><li>**Y** — смена владельца каталога.</li><li>**N** — пропустить каталог.<p>**ПРИМЕЧАНИЕ.**<br>Этот параметр следует использовать вместе с параметром **/r** .</li></ul> |
| /? | Отображение справки в командной строке. |

## <a name="remarks"></a>Комментарии

- Смешанные шаблоны с использованием (**?** и **&#42;**) не поддерживаются командой **takeown** .

- После удаления блокировки с помощью **takeown**, возможно, придется использовать проводник Windows, чтобы предоставить себе полные разрешения на доступ к файлам и каталогам, прежде чем их можно будет удалить.

## <a name="examples"></a>Примеры

Чтобы стать владельцем файла с именем *лостфиле*, введите:

```
takeown /f lostfile
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
