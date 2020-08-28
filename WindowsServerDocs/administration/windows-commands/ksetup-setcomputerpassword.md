---
title: ksetup setcomputerpassword
description: Справочная статья по команде ksetup сеткомпутерпассворд, которая задает пароль для локального компьютера.
ms.topic: reference
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdddfa424b1f34e084c9e03cb441759a64b903c1
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025378"
---
# <a name="ksetup-setcomputerpassword"></a>ksetup setcomputerpassword

Задает пароль для локального компьютера. Эта команда влияет только на учетную запись компьютера и требует перезагрузки, чтобы изменение пароля вступило в силу.

> [!IMPORTANT]
> Пароль учетной записи компьютера не отображается в реестре или в качестве выходных данных команды **ksetup** .

## <a name="syntax"></a>Синтаксис

```
ksetup /setcomputerpassword <password>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<password>` | Указывает указанный пароль для установки учетной записи компьютера на локальном компьютере. Пароль можно задать только с помощью учетной записи с правами администратора, а пароль должен содержать от 1 до 156 букв и специальных символов. |

### <a name="examples"></a>Примеры

Чтобы изменить пароль учетной записи компьютера на локальном компьютере с *IPops897* на *ИПОП $897!*, введите:

```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)
