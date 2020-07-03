---
title: bitsadmin setnotifycmdline
description: Справочная статья по команде битсадмин сетнотификмдлине, которая задает команду командной строки, которая будет выполняться, когда задание завершает передачу данных или когда задание переходит в состояние.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4466a0011f7bb1648cb7e2a51113f0a3d21c7e5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927653"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

Задает команду командной строки, которая запускается после того, как задание завершает передачу данных, или после того, как задание переходит в указанное состояние.

> [!NOTE]
> Эта команда не поддерживается в БИТАХ 1,2 и более ранних версиях.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setnotifycmdline <job> <program_name> [program_parameters]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| program_name | Имя команды, выполняемой по завершении задания. Это значение можно задать как NULL, но в этом случае *program_parameters* также должно иметь значение null. |
| program_parameters | Параметры, которые необходимо передать в *program_name*. Это значение можно задать как NULL. Если *program_parameters* не имеет значение null, первый параметр в *program_parameters* должен соответствовать *program_name*. |

## <a name="examples"></a>Примеры

Для запуска Notepad.exe по завершении задания с именем *мидовнлоаджоб*:

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe NULL
```

Чтобы отобразить текст лицензионного соглашения в Notepad.exe, по завершении задания с именем Мидовнлоаджоб:

```
bitsadmin /setnotifycmdline myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
