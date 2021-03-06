---
title: qwinsta
description: Справочная статья по команде квинста, которая отображает сведения о сеансах на сервере узла сеансов удаленный рабочий стол.
ms.topic: reference
ms.assetid: a793212a-7ecd-44cb-a77b-c5c2edb34979
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8e674f4c0384bf51a9de890b033a5734371c285a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101807517"
---
# <a name="qwinsta"></a>qwinsta

Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения о сеансах на сервере узла сеансов удаленный рабочий стол. Список включает сведения не только об активных сеансах, но и о других сеансах, которые выполняет сервер.

> [!NOTE]
> Эта команда аналогична [команде запроса Session](query-session.md). Чтобы узнать о новых возможностях последней версии, см. статью [новые возможности службы удаленных рабочих столов в Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Синтаксис

```
qwinsta [<sessionname> | <username> | <sessionID>] [/server:<servername>] [/mode] [/flow] [/connect] [/counter]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<sessionname>` | Указывает имя сеанса, с которым необходимо выполнить запрос. |
| `<username>` | Указывает имя пользователя, сеансы которого необходимо запросить. |
| `<sessionID>` | Указывает идентификатор сеанса, к которому необходимо выполнить запрос. |
| /server:`<servername>` | Определяет сервер узла сеансов удаленных рабочих столов для запроса. Значение по умолчанию — текущий сервер. |
| /Mode | Отображает текущие параметры линии. |
| /флов | Отображает текущие параметры управления потоком. |
| /коннект | Отображает текущие параметры подключения. |
| /Counter | Отображает сведения о текущих счетчиках, включая общее число созданных, отключенных и повторно подключенных сеансов. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Пользователь всегда может запрашивать сеанс, в который в данный момент вошел пользователь. Чтобы запросить другие сеансы, пользователь должен иметь специальное разрешение на доступ.

- Если вы не укажете сеанс, используя параметры <*username*>, <*Sessionname*> или *SessionID* , в этом запросе будут отображаться сведения обо всех активных сеансах в системе.

- Когда **квинста** возвращает сведения, `(>)` перед текущим сеансом отображается символ "больше чем". Например:

    ```
    C:\>qwinsta
        SESSIONNAME     USERNAME        ID STATE    TYPE    DEVICE
        console         Administrator1  0 active    wdcon
        >rdp-tcp#1      User1           1 active    wdtshare
        rdp-tcp                         2 listen    wdtshare
                                        4 idle
                                        5 idle
    ```

    Где:
  - **SESSIONNAME** указывает имя, назначенное сеансу.
  - **Username** указывает имя пользователя, подключенного к сеансу.
  - **State** предоставляет сведения о текущем состоянии сеанса.
  - **Тип** указывает тип сеанса.
  - **Устройство**, которое отсутствует для сеансов, подключенных к консоли или к сети, — это имя устройства, назначенное сеансу.
  - Все сеансы, в которых исходное состояние настроено как ОТКЛЮЧЕНное, не будут отображаться в списке **квинста** , пока они не будут включены.

### <a name="examples"></a>Примеры

Чтобы отобразить сведения обо всех активных сеансах на сервере *Server2*, введите:

```
qwinsta /server:Server2
```

Чтобы отобразить сведения о *modeM02* активного сеанса, введите:

```
qwinsta modeM02
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда "запрос сеанса"](query-session.md)

- [Справочник по командам служб удаленных рабочих столов (служб терминалов)](remote-desktop-services-terminal-services-command-reference.md)
