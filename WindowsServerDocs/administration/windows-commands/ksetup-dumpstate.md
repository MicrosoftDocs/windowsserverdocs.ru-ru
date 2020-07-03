---
title: ksetup dumpstate
description: Справочная статья по ksetup думпстате коммнанд, в которой отображается текущее состояние параметров области для всех областей, определенных на компьютере.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86e3761af14da9e1b8f52f4ce6859128fcda7bb7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929161"
---
# <a name="ksetup-dumpstate"></a>ksetup dumpstate

Отображает текущее состояние параметров области для всех областей, определенных на компьютере. Эта команда отображает те же выходные данные, что и команда **ksetup** .

## <a name="syntax"></a>Синтаксис

```
ksetup /dumpstate
```

### <a name="remarks"></a>Примечания

- Выходные данные этой команды включают область по умолчанию (домен, членом которого является компьютер) и все сферы, определенные на этом компьютере. Для каждой области предусмотрено следующее:

  - Все центры распределения ключей (Кдкс), связанные с этой областью.

  - Все флаги **области набора** для этой области.

  - Пароль KDC.

- Эта команда не отображает имя домена, указанное при обнаружении DNS или командой `ksetup /domain` .

- Эта команда не отображает пароль компьютера, установленный с помощью команды `ksetup /setcomputerpassword` .

## <a name="examples"></a>Примеры

Чтобы выбрать конфигурацию области Kerberos на компьютере, введите:

```
ksetup /dumpstate
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)