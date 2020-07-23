---
title: wbadmin restore catalog
description: Справочная статья по Wbadmin Recover Catalog, которая восстанавливает каталог резервных копий для локального компьютера из указанного места хранения.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a31fb2a49e5a85f7fdb4b8b5a7becc8ea57e13d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954601"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore catalog

Восстанавливает каталог резервных копий для локального компьютера из указанного места хранения.

Чтобы восстановить каталог резервных копий с помощью этой подкоманды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями. (Чтобы открыть командную строку с повышенными привилегиями, щелкните правой кнопкой мыши пункт **Командная строка**и выберите команду **Запуск от имени администратора**.)

## <a name="syntax"></a>Синтаксис

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|-backupTarget|Указывает расположение каталога резервных копий системы в том виде, в котором он находился в момент создания резервной копии.|
|-Machine|Указывает имя компьютера, для которого требуется восстановить каталог резервных копий. Используется при хранении резервных копий на нескольких компьютерах в одном и том же месте. Следует использовать, если указан **-backupTarget** .|
|-quiet|Выполняет подкоманду без запросов пользователю.|

## <a name="remarks"></a>Комментарии

Если расположение (диск, DVD или удаленная общая папка), где хранятся резервные копии, повреждено или утеряно и не может использоваться для восстановления каталога резервного копирования, используйте **Wbadmin Delete Catalog** , чтобы удалить поврежденный каталог. В этом случае следует создать новую резервную копию после удаления каталога резервного копирования.

## <a name="examples"></a>Примеры

Чтобы восстановить каталог из резервной копии, хранящейся на диске d:, введите:
```
wbadmin restore catalog -backupTarget:d
```
Чтобы восстановить каталог из резервной копии, хранящейся в общей папке \\ \\ сервернаме\шаре Server01, введите:
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   Командлет [RESTORE-вбкаталог](/powershell/module/windowserverbackup/?view=winserver2012r2-ps)
