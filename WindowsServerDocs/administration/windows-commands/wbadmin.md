---
title: wbadmin
description: Раздел команд Windows для Wbadmin, который позволяет выполнять резервное копирование и восстановление операционной системы, томов, файлов, папок и приложений из командной строки.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ca9bdc54cd77f11239d0a61cf052e7b12b02b22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829477"
---
# <a name="wbadmin"></a>wbadmin



Позволяет выполнять резервное копирование и восстановление операционной системы, томов, файлов, папок и приложений из командной строки.

Чтобы настроить регулярное запланированное резервное копирование, необходимо быть членом группы **администраторов** . Для выполнения всех других задач с помощью этой команды необходимо быть членом группы " **Операторы резервного копирования** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения.

Необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями. (Чтобы открыть командную строку с повышенными привилегиями, щелкните правой кнопкой мыши пункт **Командная строка**и выберите команду **Запуск от имени администратора**.)

## <a name="subcommands"></a>Подкоманды

|Подкоманда|Описание|
|----------|-----------|
|[Wbadmin enable backup](wbadmin-enable-backup.md)|Настраивает и включает регулярное запланированное резервное копирование.|
|[Wbadmin disable backup](wbadmin-disable-backup.md)|Отключает ежедневное резервное копирование.|
|[Wbadmin start backup](wbadmin-start-backup.md)|Выполняет однократную архивацию. При использовании без параметров использует параметры из расписания ежедневного резервного копирования.|
|[Wbadmin stop job](wbadmin-stop-job.md)|Останавливает текущую выполняемую операцию резервного копирования или восстановления.|
|[Wbadmin get versions](wbadmin-get-versions.md)|Выводит сведения об восстанавливаемых резервных копиях с локального компьютера или, если указано другое расположение, с другого компьютера.|
|[Wbadmin get items](wbadmin-get-items.md)|Список элементов, входящих в резервную копию.|
|[Wbadmin start recovery](wbadmin-start-recovery.md)|Выполняет восстановление указанных томов, приложений, файлов или папок.|
|[Wbadmin get status](wbadmin-get-status.md)|Отображает состояние выполняемой в данный момент операции резервного копирования или восстановления.|
|[Wbadmin get disks](wbadmin-get-disks.md)|Выводит список дисков, находящихся в режиме в сети.|
|[Wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md)|Выполняет восстановление состояния системы.|
|[Wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md)|Выполняет резервное копирование состояния системы.|
|[Wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md)|Удаляет одну или несколько резервных копий состояния системы.|
|[Wbadmin start sysrecovery](wbadmin-start-sysrecovery.md)|Выполняет восстановление всей системы (по крайней мере все тома, содержащие состояние операционной системы). Эта подкоманда доступна только при использовании среды восстановления Windows.|
|[Wbadmin restore catalog](wbadmin-restore-catalog.md)|Восстанавливает каталог резервных копий из указанного места хранения в случае повреждения каталога резервного копирования на локальном компьютере.|
|[Wbadmin delete catalog](wbadmin-delete-catalog.md)|Удаляет каталог резервных копий на локальном компьютере. Используйте эту подкоманду только в том случае, если каталог резервного копирования на этом компьютере поврежден и резервные копии не хранятся в другом расположении, которое можно использовать для восстановления каталога.|

## <a name="additional-references"></a>Дополнительные материалы

-   [Резервное копирование и восстановление](https://go.microsoft.com/fwlink/?LinkID=195054)
-   [cистема архивации данных Windows Server командлетов в Windows PowerShell](https://technet.microsoft.com/library/jj902428.aspx)