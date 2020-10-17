---
title: wbadmin restore catalog
description: Справочная статья по команде Wbadmin Recover Catalog, которая восстанавливает каталог резервных копий для локального компьютера из указанного места хранения.
ms.topic: reference
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 046c4b4162c9512d5893c3c06e83e7260386c990
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155868"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore catalog

Восстанавливает каталог резервных копий для локального компьютера из указанного места хранения.

Чтобы восстановить каталог резервных копий, включенный в определенную резервную копию с помощью этой команды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши **командную строку**и выбрав команду **Запуск от имени администратора**.

> [!NOTE]
> Если расположение (диск, DVD или удаленная общая папка), где хранятся резервные копии, повреждено или утеряно, и его нельзя использовать для восстановления каталога резервного копирования, выполните команду [Wbadmin Delete Catalog](wbadmin-delete-catalog.md) , чтобы удалить поврежденный каталог. В этом случае рекомендуется создать новую резервную копию после удаления каталога резервного копирования.

## <a name="syntax"></a>Синтаксис

```
wbadmin restore catalog -backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>} [-machine:<BackupMachineName>] [-quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -backupTarget | Указывает расположение каталога резервных копий системы в том виде, в котором он находился в момент создания резервной копии. |
| -Machine | Указывает имя компьютера, для которого требуется восстановить каталог резервных копий. Используется при хранении резервных копий на нескольких компьютерах в одном и том же месте. Следует использовать, если указан **-backupTarget** . |
| -quiet | Выполняет команду без запроса пользователю. |

## <a name="examples"></a>Примеры

Чтобы восстановить каталог из резервной копии, хранящейся на диске D:, введите:

```
wbadmin restore catalog -backupTarget:D
```

Чтобы восстановить каталог из резервной копии, хранящейся в общей папке `\\<servername>\<share>` Server01, введите:

```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Wbadmin](wbadmin.md)

- [Команда Wbadmin Delete Catalog](wbadmin-delete-catalog.md)

- [Restore-Вбкаталог](/powershell/module/windowserverbackup/Restore-WBCatalog)
