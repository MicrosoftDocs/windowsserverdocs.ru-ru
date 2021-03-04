---
title: wbadmin
description: Справочная статья по командам Wbadmin, которая позволяет выполнять резервное копирование и восстановление операционной системы, томов, файлов, папок и приложений из командной строки.
ms.topic: reference
ms.assetid: 4b0b3f32-d21f-4861-84bb-b2eadbf1e7b8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ae5595866bfa819ed63831d85a395b1659d9e716
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804317"
---
# <a name="wbadmin"></a>wbadmin

Позволяет выполнять резервное копирование и восстановление операционной системы, томов, файлов, папок и приложений из командной строки.

Чтобы настроить регулярное запланированное резервное копирование с помощью этой команды, необходимо быть членом группы " **Администраторы** ". Для выполнения всех других задач с помощью этой команды необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения.

Необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши пункт **Командная строка** и выбрав команду **Запуск от имени администратора**.

## <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [wbadmin delete catalog](wbadmin-delete-catalog.md) | Удаляет каталог резервных копий на локальном компьютере. Используйте эту команду только в том случае, если каталог резервного копирования на этом компьютере поврежден и резервные копии не хранятся в другом расположении, которое можно использовать для восстановления каталога. |
| [wbadmin delete systemstatebackup](wbadmin-delete-systemstatebackup.md) | Удаляет одну или несколько резервных копий состояния системы. |
| [wbadmin disable backup](wbadmin-disable-backup.md) | Отключает ежедневное резервное копирование. |
| [wbadmin enable backup](wbadmin-enable-backup.md) | Настраивает и включает регулярное запланированное резервное копирование. |
| [wbadmin get disks](wbadmin-get-disks.md) | Выводит список дисков, находящихся в режиме в сети. |
| [wbadmin get items](wbadmin-get-items.md) | Список элементов, входящих в резервную копию. |
| [wbadmin get status](wbadmin-get-status.md) | Отображает состояние выполняемой в данный момент операции резервного копирования или восстановления. |
| [wbadmin get versions](wbadmin-get-versions.md) | Выводит сведения об восстанавливаемых резервных копиях с локального компьютера или, если указано другое расположение, с другого компьютера. |
| [wbadmin restore catalog](wbadmin-restore-catalog.md) | Восстанавливает каталог резервных копий из указанного места хранения в случае повреждения каталога резервного копирования на локальном компьютере. |
| [wbadmin start backup](wbadmin-start-backup.md) | Выполняет однократную архивацию. При использовании без параметров использует параметры из расписания ежедневного резервного копирования. |
| [wbadmin start recovery](wbadmin-start-recovery.md) | Выполняет восстановление указанных томов, приложений, файлов или папок. |
| [wbadmin start sysrecovery](wbadmin-start-sysrecovery.md) | Выполняет восстановление всей системы (по крайней мере все тома, содержащие состояние операционной системы). Эта команда доступна только при использовании среды восстановления Windows. |
| [wbadmin start systemstatebackup](wbadmin-start-systemstatebackup.md) | Выполняет резервное копирование состояния системы. |
| [wbadmin start systemstaterecovery](wbadmin-start-systemstaterecovery.md) | Выполняет восстановление состояния системы. |
| [wbadmin stop job](wbadmin-stop-job.md) | Останавливает текущую выполняемую операцию резервного копирования или восстановления. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [cистема архивации данных Windows Server командлетов в Windows PowerShell](/powershell/module/windowsserverbackup)

- [Среда восстановления Windows (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
