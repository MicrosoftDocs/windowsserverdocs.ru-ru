---
title: wbadmin delete catalog
description: Справочная статья по команде Wbadmin Delete Catalog, которая удаляет каталог резервных копий, хранящийся на локальном компьютере.
ms.topic: reference
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4a19d856b65fdcf17fb369d81607445530f77275
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156103"
---
# <a name="wbadmin-delete-catalog"></a>wbadmin delete catalog

Удаляет каталог резервных копий, хранящийся на локальном компьютере. Используйте эту команду, если каталог резервного копирования поврежден и вы не можете восстановить его с помощью команды [Wbadmin Restore Catalog](wbadmin-restore-catalog.md) .

Чтобы удалить каталог резервных копий с помощью этой команды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши **командную строку**и выбрав команду **Запуск от имени администратора**.

## <a name="syntax"></a>Синтаксис

```
wbadmin delete catalog [-quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -quiet | Выполняет команду без запроса пользователю. |

#### <a name="remarks"></a>Комментарии

- Если удалить каталог резервных копий компьютера, вы больше не сможете получить доступ к резервным копиям, созданным для этого компьютера, с помощью оснастки cистема архивации данных Windows Server. Однако если вы можете получить другое расположение резервной копии и выполнить команду [Wbadmin Restore Catalog](wbadmin-restore-catalog.md) , можно восстановить каталог резервных копий из этого расположения.

- Настоятельно рекомендуется создать новую резервную копию после удаления каталога резервного копирования.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Wbadmin](wbadmin.md)

- [Команда Wbadmin Restore Catalog](wbadmin-restore-catalog.md)

- [Remove-Вбкаталог](/powershell/module/windowsserverbackup/Remove-WBCatalog)
