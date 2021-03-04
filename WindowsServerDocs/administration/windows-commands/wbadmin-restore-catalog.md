---
title: wbadmin restore catalog
description: Справочная статья по команде Wbadmin Recover Catalog, которая восстанавливает каталог резервных копий для локального компьютера из указанного места хранения.
ms.topic: reference
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3e3cabbf43c8b54a51d2a4d1309b069b24ea70a0
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804447"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore catalog

Восстанавливает каталог резервных копий для локального компьютера из указанного места хранения.

Чтобы восстановить каталог резервных копий, включенный в определенную резервную копию с помощью этой команды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши **командную строку** и выбрав команду **Запуск от имени администратора**.

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
