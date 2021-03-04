---
title: wbadmin start systemstatebackup
description: Справочная статья по команде Wbadmin start системстатебаккуп, которая создает резервную копию состояния системы локального компьютера и сохраняет ее в указанном расположении.
ms.topic: reference
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a5da108b277037609e5c6ad7ebeddae9c5e9fcb8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804347"
---
# <a name="wbadmin-start-systemstatebackup"></a>wbadmin start systemstatebackup

Создает резервную копию состояния системы локального компьютера и сохраняет ее в указанном расположении.

Чтобы выполнить резервное копирование состояния системы с помощью этой команды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши **командную строку** и выбрав команду **Запуск от имени администратора**.

> [!NOTE]
> Cистема архивации данных Windows Server не выполняет резервное копирование и восстановление кустов пользователя реестра (HKEY_CURRENT_USER) в ходе резервного копирования состояния системы или восстановления состояния системы.

## <a name="syntax"></a>Синтаксис

```
wbadmin start systemstatebackup -backupTarget:<VolumeName> [-quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -backupTarget | Указывает расположение, в котором будет храниться резервная копия. Для расположения хранилища требуется буква диска или том на основе GUID в формате: `\\?\Volume{*GUID*}` . Используйте команду `-backuptarget:\\servername\sharedfolder\` для хранения резервных копий состояния системы. |
| -quiet | Выполняет команду без запроса пользователю. |

## <a name="examples"></a>Примеры

Чтобы создать резервную копию состояния системы и сохранить ее на томе f, введите:

```
wbadmin start systemstatebackup -backupTarget:f:
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Wbadmin](wbadmin.md)

- [Start-Вббаккуп](/powershell/module/windowserverbackup/Start-WBBackup)
