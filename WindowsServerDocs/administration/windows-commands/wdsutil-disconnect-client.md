---
title: WDSUTIL Disconnect — клиент
description: Справочная статья по команде WDSUTIL Disconnect-Client, которая отключает клиент от многоадресной передачи или пространства имен.
ms.topic: reference
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd837fd9a677f78b5890cd1f2092529d44a2bc68
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070336"
---
# <a name="wdsutil-disconnect-client"></a>WDSUTIL Disconnect — клиент

Отключает клиент от многоадресной передачи или пространства имен. Если не указано значение **/Force** , клиент будет возвращаться к другому методу передачи (если он поддерживается клиентом).

## <a name="syntax"></a>Синтаксис

```
wdsutil /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| ClientID`<ClientID>` | Указывает идентификатор клиента, который должен быть отключен. Чтобы просмотреть идентификатор клиента, выполните `wdsutil /get-multicasttransmission /show:clients` команду. |
| [/Server: `<Servername>` ] | Указывает имя сервера. Это может быть NetBIOS-имя или полное доменное имя (FQDN). Если имя сервера не указано, используется локальный сервер. |
| /Force | Полностью останавливает установку и не использует резервный метод. Поскольку Wdsmcast.exe не поддерживает никаких резервных механизмов, поведение по умолчанию выглядит следующим образом:<ul><li>**Если вы используете клиент служб развертывания Windows, выполните следующие действия.** Клиент продолжит установку с помощью одноадресной рассылки.</li><li>**Если вы не используете клиент служб развертывания Windows, выполните следующие действия.** Установка завершается сбоем.</li></ul>**Важно.** Мы настоятельно рекомендуем использовать этот параметр с осторожностью, так как в случае сбоя установки компьютер может остаться в неработоспособном состоянии. |

## <a name="examples"></a>Примеры

Чтобы отключить клиент, введите:

```
wdsutil /Disconnect-Client /ClientId:1
```

Чтобы отключить клиент и принудительно завершить установку, введите:

```
wdsutil /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда WDSUTIL Get-мултикасттрансмиссион](wdsutil-get-multicasttransmission.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
