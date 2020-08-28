---
title: ksetup dumpstate
description: Справочная статья по ksetup думпстате коммнанд, в которой отображается текущее состояние параметров области для всех областей, определенных на компьютере.
ms.topic: reference
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8723eac23cc2444bf4c16a661b13cc8cef4798dc
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025528"
---
# <a name="ksetup-dumpstate"></a>ksetup dumpstate

Отображает текущее состояние параметров области для всех областей, определенных на компьютере. Эта команда отображает те же выходные данные, что и команда **ksetup** .

## <a name="syntax"></a>Синтаксис

```
ksetup /dumpstate
```

### <a name="remarks"></a>Remarks

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