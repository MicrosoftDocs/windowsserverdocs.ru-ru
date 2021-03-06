---
title: Команды Netsh для порта прокси-сервера интерфейса
description: Используйте команды порта прокси-сервера интерфейса Netsh, чтобы действовать в качестве прокси-серверов в сетях IPv4, IPv6 и приложениях.
ms.topic: article
manager: dougkim
ms.author: jgerend
author: JasonGerend
ms.date: 08/30/2018
ms.openlocfilehash: ca8e5f92fb4322f5e4baf49b3f26a94ea4858c27
ms.sourcegitcommit: 09f664580714bc46f91771907a2e3ce7018bfb9d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2021
ms.locfileid: "102237736"
---
# <a name="netsh-interface-portproxy-commands"></a>Команды порта прокси-сервера интерфейса Netsh

Используйте **команды порта прокси-сервера интерфейса Netsh**, чтобы действовать в качестве прокси-серверов в сетях IPv4, IPv6 и приложениях. Эти команды можно использовать для установки прокси-службы следующими способами:

-   Сообщения компьютера и приложения, настроенных по протоколу IPv4, отправлены другим компьютерам и приложениям, настроенным по протоколу IPv4.

-   Сообщения компьютера и приложения, настроенных по протоколу IPv4, отправлены компьютерам и приложениям, настроенным по протоколу IPv6.

-   Сообщения компьютера и приложения, настроенных по протоколу IPv6, отправлены компьютерам и приложениям, настроенным по протоколу IPv4.

-   Сообщения компьютера и приложения, настроенных по протоколу IPv6, отправлены другим компьютерам и приложениям, настроенным по протоколу IPv6.

Используя эти команды при записи пакетных файлов или скриптов, каждая команда должна начинаться с **netsh interface portproxy**. Например, при использовании команды **delete v4tov6**, чтобы указать, что прокси-сервер порта удаляет порт IPv4 и адрес из списка IPv4-адресов, прослушиваемых сервером, в пакетном файле или скрипте должен использоваться следующий синтаксис:

```PowerShell
netsh interface portproxy delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

Доступны следующие команды порта прокси-сервера интерфейса netsh:

-   [add v4tov4](#add-v4tov4);

-   [add v4tov6](#add-v4tov6);

-   [add v6tov4](#add-v6tov4);

-   [add v6tov6](#add-v6tov6);

-   [delete v4tov4](#delete-v4tov4);

-   [delete v4tov6](#delete-v4tov6);

-   [delete v6tov6](#delete-v6tov6);

-   [reset](#reset);

-   [set v4tov4](#set-v4tov4);

-   [set v4tov6](#set-v4tov6);

-   [setv6tov4](#set-v6tov4);

-   [set v6tov6](#set-v6tov6);

-   [show all](#show-all);

-   [show v4tov4](#show-v4tov4);

-   [show v4tov6](#show-v4tov6);

-   [show v6tov4](#show-v6tov4);

-   [show v6tov6](#show-v6tov6).


## <a name="add-v4tov4"></a>Команда add v4tov4

Прокси-сервер порта прослушивает сообщения, отправленные на указанный порт и IPv4-адрес, а затем сопоставляет порт и IPv4-адрес, чтобы отправить сообщения, полученные после установки отдельного TCP-соединения.

### <a name="syntax"></a>Синтаксис

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv4 по номеру порта или имени службы, который будет прослушиваться.                                                            |
| **connectaddress** | Указывает IPv4-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv4 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv4-адрес, который должен прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="add-v4tov6"></a>Команда add v4tov6

Прокси-сервер порта прослушивает сообщения, отправленные на указанный порт и IPv4-адрес, а затем сопоставляет порт и IPv6-адрес, чтобы отправить сообщения, полученные после установки отдельного TCP-соединения.

### <a name="syntax"></a>Синтаксис

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv4 по номеру порта или имени службы, который будет прослушиваться.                                                            |
| **connectaddress** | Указывает IPv6-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv6 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv4-адрес, который будет прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера.  |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="add-v6tov4"></a>Команда add v6tov4

Прокси-сервер порта прослушивает сообщения, отправленные на указанный порт и IPv6-адрес, а затем сопоставляет порт и IPv4-адрес, чтобы отправить сообщения, полученные после установки отдельного TCP-соединения.

### <a name="syntax"></a>Синтаксис

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv6 по номеру порта или имени службы, который следует прослушивать.                                                            |
| **connectaddress** | Указывает IPv4-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv4 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv6-адрес, который должен прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера.  |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="add-v6tov6"></a>Команда add v6tov6

Прокси-сервер порта прослушивает сообщения, отправленные на указанный порт и IPv6-адрес, а затем сопоставляет порт и IPv6-адрес, чтобы отправить сообщения, полученные после установки отдельного TCP-соединения.

### <a name="syntax"></a>Синтаксис

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv6 по номеру порта или имени службы, который следует прослушивать.                                                            |
| **connectaddress** | Указывает IPv6-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv6 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv6-адрес, который должен прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера.  |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="delete-v4tov4"></a>Команда delete v4tov4

Прокси-сервер порта удаляет IPv4-адрес из списка IPv4-портов и адресов, которые прослушивает сервер.

### <a name="syntax"></a>Синтаксис

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Указывает удаляемый IPv4-порт.                                    |
| **listenaddress** | Указывает удаляемый IPv4-адрес. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|   **protocol**    |                                      Указывает протокол, который необходимо использовать.                                      |

## <a name="delete-v4tov6"></a>Команда delete v4tov6

Прокси-сервер порта удаляет IPv4-порт и адрес из списка IPv4-адресов, которые прослушивает сервер.

### <a name="syntax"></a>Синтаксис

```PowerShell
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Указывает удаляемый IPv4-порт.                                    |
| **listenaddress** | Указывает удаляемый IPv4-адрес. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|   **protocol**    |                                      Указывает протокол, который необходимо использовать.                                      |

## <a name="delete-v6tov4"></a>Команда delete v6tov4

Прокси-сервер порта удаляет IPv6-порт и адрес из списка IPv6-адресов, прослушиваемых на сервере.

### <a name="syntax"></a>Синтаксис

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Указывает удаляемый IPv6-порт.                                    |
| **listenaddress** | Указывает удаляемый адрес IPv6-адрес. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|   **protocol**    |                                      Указывает протокол, который необходимо использовать.                                      |

## <a name="delete-v6tov6"></a>Команда delete v6tov6

Прокси-сервер порта удаляет IPv6-адрес из списка IPv6-адресов, которые прослушивает сервер.

### <a name="syntax"></a>Синтаксис

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Указывает удаляемый IPv6-порт.                                    |
| **listenaddress** | Указывает удаляемый адрес IPv6-адрес. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|   **protocol**    |                                      Указывает протокол, который необходимо использовать.                                      |

## <a name="reset"></a>сброс

Сбрасывает состояние конфигурации IPv6.

### <a name="syntax"></a>Синтаксис

`reset`

## <a name="set-v4tov4"></a>Команда set v4tov4

Изменяет значения параметров имеющейся записи на прокси-сервере порта, созданной с помощью команды **add v4tov4**, или добавляет новую запись в список, который сопоставляет пары портов и адресов.

### <a name="syntax"></a>Синтаксис

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv4 по номеру порта или имени службы, который будет прослушиваться.                                                            |
| **connectaddress** | Указывает IPv4-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv4 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv4-адрес, который должен прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="set-v4tov6"></a>Команда set v4tov6

Изменяет значения параметров существующей записи на прокси-сервере порта, созданной с помощью команды **add v4tov6**, или добавляет новую запись в список, который сопоставляет пары портов и адресов.

### <a name="syntax"></a>Синтаксис

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv4 по номеру порта или имени службы, который будет прослушиваться.                                                            |
| **connectaddress** | Указывает IPv6-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv6 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv4-адрес, который будет прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера.  |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="set-v6tov4"></a>Команда set v6tov4

Изменяет значения параметров существующей записи на прокси-сервере порта, созданной с помощью команды **add v6tov4**, или добавляет новую запись в список, который сопоставляет пары портов и адресов.

### <a name="syntax"></a>Синтаксис

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Указывает порт IPv6 по номеру порта или имени службы, который следует прослушивать.                                                            |
| **connectaddress** | Указывает IPv4-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера. |
|  **connectport**   |       Указывает порт IPv4 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv6-адрес, который должен прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера.  |
|    **protocol**    |                                                                                  Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="set-v6tov6"></a>Команда set v6tov6

Изменяет значения параметров существующей записи на прокси-сервере порта, созданной с помощью команды **Add v6tov6**, или добавляет новую запись в список, который сопоставляет пары портов и адресов.

### <a name="syntax"></a>Синтаксис

```PowerShell
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>Параметры

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                            Указывает порт IPv6 по номеру порта или имени службы, который следует прослушивать.                                                            |
| **connectaddress** | Указывает IPv6-адрес, к которому необходимо подключиться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если адрес не указан, по умолчанию используется адрес локального компьютера.  |
|  **connectport**   |        Указывает порт IPv6 по номеру порта или имени службы, к которому необходимо подключиться. Если значение **connectport** не указано, по умолчанию на локальном компьютере используется значение **listenport**.        |
| **listenaddress**  | Указывает IPv6-адрес, который должен прослушиваться. Допустимые значения: IP-адрес, имя NetBIOS или DNS-имя компьютера. Если вы не указали адрес, по умолчанию используется адрес локального компьютера. |
|    **protocol**    |                                                                                   Указывает протокол, который необходимо использовать.                                                                                   |

## <a name="show-all"></a>показать все

Отображает все параметры порта прокси-сервера, включая пары портов и адресов для v4tov4, v4tov6, v6tov4 и v6tov6.

### <a name="syntax"></a>Синтаксис

`show all`


## <a name="show-v4tov4"></a>Команда show v4tov4

Отображает параметры прокси-сервера порта v4tov4.

### <a name="syntax"></a>Синтаксис

`show v4tov4`

## <a name="show-v4tov6"></a>Команда show v4tov6

Отображает параметры прокси-сервера порта v4tov6.

### <a name="syntax"></a>Синтаксис

`show v4tov6`

## <a name="show-v6tov4"></a>Команда show v6tov4

Отображает параметры прокси-сервера порта v6tov4.

### <a name="syntax"></a>Синтаксис

`show v6tov4`


## <a name="show-v6tov6"></a>Команда show v6tov6

Отображает параметры прокси-сервера порта v6tov6.

### <a name="syntax"></a>Синтаксис

`show v6tov6`

---
