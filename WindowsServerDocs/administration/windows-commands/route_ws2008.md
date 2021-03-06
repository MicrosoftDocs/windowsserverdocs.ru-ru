---
title: route
description: Справочная статья по команде Route, которая изменяет и отображает записи в локальной таблице маршрутизации IP.
ms.topic: reference
ms.assetid: afcd666c-0cef-47c2-9bcc-02d202b983b3
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: dc440d66ae4e3d729494060c7a7c63b4eb841dfb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806777"
---
# <a name="route"></a>route

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает и изменяет записи в локальной таблице маршрутизации IP. Если используется без параметров, команда **Route** выводит справку из командной строки.

> [!IMPORTANT]
> Эта команда доступна, только если протокол Internet Protocol (TCP/IP) установлен в качестве компонента в свойствах сетевого адаптера в окне Сетевые подключения.

## <a name="syntax"></a>Синтаксис

```
route [/f] [/p] [<command> [<destination>] [mask <netmask>] [<gateway>] [metric <metric>]] [if <interface>]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /f | Очищает таблицу маршрутизации всех записей, не являющихся маршрутами узла (маршруты с сетевой маской 255.255.255.255), маршрутом сети замыкания на себя (маршруты с назначением 127.0.0.0 и сетевой маской 255.0.0.0) или маршрутом многоадресной рассылки (маршруты с назначением 224.0.0.0 и сетевой маской 240.0.0.0). Если используется в сочетании с одной из команд (например, Add, Change или DELETE), таблица удаляется перед выполнением команды. |
| /p | При использовании с командой Add указанный маршрут добавляется в реестр и используется для инициализации таблицы IP-маршрутизации при каждом запуске протокола TCP/IP. По умолчанию при запуске протокола TCP/IP добавленные маршруты не сохраняются. При использовании с командой print отображается список постоянных маршрутов. Этот параметр игнорируется для всех остальных команд. Постоянные маршруты хранятся в папке реестра **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\PersistentRoutes**. |
| `<command>` | Указывает команду, которую требуется выполнить. К допустимым командам относятся:<ul><li>**Добавить** — добавляет маршрут.</li><li>**Change** — изменяет существующий маршрут.</li><li>**Удалить:** — удаляет маршрут или маршруты.</li><li>**Печать** — печать маршрута или маршрутов.</li></ul> |
| `<destination>` | Указывает сетевой адрес маршрута. Назначением может быть IP-адрес сети (где биты узла сетевого адреса имеют значение 0), IP-адрес для маршрута узла или 0.0.0.0 для маршрута по умолчанию. |
| виде `<netmask>` | Указывает сетевой адрес маршрута. Назначением может быть IP-адрес сети (где биты узла сетевого адреса имеют значение 0), IP-адрес для маршрута узла или 0.0.0.0 для маршрута по умолчанию. |
| `<gateway>` | Указывает IP-адрес перенаправления или следующего прыжка, по которому можно получить набор адресов, определяемых назначением сети и маской подсети. Для локально подключенных маршрутов подсети адрес шлюза — это IP-адрес, назначенный интерфейсу, подключенному к подсети. Для удаленных маршрутов, доступных на одном или нескольких маршрутизаторах, адрес шлюза представляет собой напрямую достижимый IP-адрес, назначенный соседнему маршрутизатору. |
| шкал `<metric>` | Указывает целочисленную метрику стоимости (от 1 до 9999) для маршрута, который используется при выборе нескольких маршрутов в таблице маршрутизации, наиболее точно соответствующих адресу назначения перенаправляемого пакета. Выбирается маршрут с наименьшей метрикой. Метрика может отражать число прыжков, скорость пути, надежность пути, пропускную способность пути или административные свойства. |
| наличии `<interface>` | Указывает индекс интерфейса для интерфейса, для которого целевой объект доступен. Чтобы получить список интерфейсов и их соответствующих индексов интерфейсов, используйте отображение команды route print. Для индекса интерфейса можно использовать либо десятичное, либо шестнадцатеричное значение. Для шестнадцатеричных значений перед шестнадцатеричным числом следует указать 0x. Если параметр if опущен, интерфейс определяется по адресу шлюза. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Большие значения в столбце **метрик** таблицы маршрутизации являются результатом того, что TCP/IP автоматически определяет метрику маршрутов в таблице маршрутизации на основе конфигурации IP-адреса, маски подсети и шлюза по умолчанию для каждого интерфейса локальной сети. Автоматическое определение метрики интерфейса, включенное по умолчанию, определяет скорость каждого интерфейса и корректирует метрики маршрутов для каждого интерфейса, чтобы самый быстрый интерфейс создавал маршруты с наименьшей метрикой. Чтобы удалить большие метрики, отключите автоматическое определение метрики интерфейса из дополнительных свойств протокола TCP/IP для каждого подключения к локальной сети.

- Имена могут использоваться для *назначения* , если в файле локальных *сетей* , хранящемся в папке, есть соответствующая запись `systemroot\System32\Drivers\\` . Имена могут использоваться для *шлюза* при условии, что они могут быть разрешены по IP-адресу с помощью стандартных методов разрешения имен узлов, таких как запросы службы доменных имен (DNS), использование локального файла Hosts, хранящегося в `systemroot\system32\drivers\\` папке, и разрешение имен NetBIOS.

- Если команда **печатается** или **удаляется**, параметр *шлюза* можно опустить, а для назначения и шлюза можно использовать подстановочные знаки. *Конечным* значением может быть подстановочное значение, заданное звездочкой `(*)` . Если указанное назначение содержит звездочку или вопросительный `(*)` знак (?), оно рассматривается как подстановочный знак и печатается или удаляется только в соответствующих маршрутах назначения. Звездочка соответствует любой строке, а вопросительный знак соответствует любому отдельному символу. Например,, `10.\*.1, 192.168.\*` `127.\*` и `\*224\*` являются допустимыми символами-шаблонами звездочки.

- При использовании неподдерживаемого сочетания назначения и маски подсети (маска) отображается сообщение об ошибке "маршрут: неправильная Маска адреса шлюза". Это сообщение об ошибке появляется, если назначение содержит одну или несколько битов, равных 1 в битах, где соответствующий бит маски подсети имеет значение 0. Чтобы протестировать это условие, выразит назначение и маску подсети с помощью двоичной нотации. Маска подсети в двоичной нотации состоит из последовательности из 1 бит, представляющей часть сетевого адреса назначения, и серии из 0 бит, представляющих часть адреса узла назначения. Установите флажок, чтобы определить наличие в назначении битов, для которых задано значение 1, для части назначения, которая является адресом узла (как определено маской подсети).

## <a name="examples"></a>Примеры

Чтобы отобразить все содержимое таблицы IP-маршрутизации, введите:

```
route print
```

Чтобы отобразить маршруты в таблице IP-маршрутизации, начинающейся с 10, введите:

```
route print 10.*
```

Чтобы добавить маршрут по умолчанию с адресом шлюза по умолчанию 192.168.12.1, введите:

```
route add 0.0.0.0 mask 0.0.0.0 192.168.12.1
```

Чтобы добавить маршрут к целевому 10.41.0.0 с маской подсети 255.255.0.0 и адресом следующего прыжка 10.27.0.1, введите:

```
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1
```

Чтобы добавить постоянный маршрут к целевому 10.41.0.0 с маской подсети 255.255.0.0 и адресом следующего прыжка 10.27.0.1, введите:

```
route /p add 10.41.0.0 mask 255.255.0.0 10.27.0.1
```

Чтобы добавить маршрут к целевому 10.41.0.0 с маской подсети 255.255.0.0, адрес следующего прыжка 10.27.0.1 и метрику стоимости 7, введите:

```
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 metric 7
```

Чтобы добавить маршрут к целевому 10.41.0.0 с маской подсети 255.255.0.0, адрес следующего прыжка 10.27.0.1, а также используя интерфейс 0x3 индекса, введите:

```
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 if 0x3
```

Чтобы удалить маршрут к целевому 10.41.0.0 с маской подсети 255.255.0.0, введите:

```
route delete 10.41.0.0 mask 255.255.0.0
```

Чтобы удалить все маршруты в таблице IP-маршрутизации, начинающейся с 10, введите:

```
route delete 10.*
```

Чтобы изменить адрес следующего прыжка маршрута с назначением 10.41.0.0 и маской подсети 255.255.0.0 с 10.27.0.1 на 10.27.0.25, введите:

```
route change 10.41.0.0 mask 255.255.0.0 10.27.0.25
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
