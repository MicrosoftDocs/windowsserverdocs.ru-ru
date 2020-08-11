---
title: Пример пакетного файла сетевой оболочки (Netsh)
description: В этой статье вы узнаете, как создать пакетный файл, выполняющий несколько задач в оболочке Netsh на Windows Server 2016.
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 35690e25fa18512d729bbd323b8983284a41781d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953980"
---
# <a name="network-shell-netsh-example-batch-file"></a>Пример пакетного файла сетевой оболочки (Netsh)

Область применения. Windows Server 2016

В этой статье вы узнаете, как создать пакетный файл, выполняющий несколько задач в оболочке Netsh на Windows Server 2016. В этом примере пакетного файла используется контекст **netsh wins**.

## <a name="example-batch-file-overview"></a>Общие сведения о примере пакетного файла

Вы можете использовать команды Netsh для службы \(WINS\) (Windows Internet Name Service) в пакетных файлах и других скриптах для автоматизации задач. В следующем примере пакетного файла показано, как с помощью команд Netsh для WINS выполнять несколько однотипных задач.

В этом примере пакетного файла WINS\-A обозначает WINS-сервер с IP-адресом 192.168.125.30, а WINS\-B — WINS-сервер с IP-адресом 192.168.0.189.

Этот пример пакетного файла выполняет следующие задачи.

- Добавляет динамическую запись имени для IP-адреса 192.168.0.205, MY\_RECORD \[04h\], на сервер WINS\-A.
- Устанавливает WINS\-B в качестве партнера по извещающей или опрашивающей репликации для WINS\-A.
- Подключается к WINS\-B и устанавливает WINS\-A в качестве партнера по извещающей или опрашивающей репликации для WINS\-B.
- Инициирует извещающую репликацию из WINS\-A в WINS\-B.
- Подключается к WINS\-B и проверяет успешность репликации новой записи MY\_RECORD.

## <a name="netsh-example-batch-file"></a>Примере пакетного файла netsh

В следующем примере пакетного файла в строки с комментариями добавлен префикс "rem". Оболочка netsh игнорирует такие комментарии.

```
rem: Begin example batch file.
rem two WINS servers:
rem (WINS-A) 192.168.125.30
rem (WINS-B) 192.168.0.189

rem 1. Connect to (WINS-A), and add the dynamic name MY\_RECORD \[04h\] to the (WINS-A) database.
netsh wins server 192.168.125.30 add name Name=MY\_RECORD EndChar=04 IP={192.168.0.205}

rem 2. Connect to (WINS-A), and set (WINS-B) as a push/pull replication partner of (WINS-A).
netsh wins server 192.168.125.30 add partner Server=192.168.0.189 Type=2

rem 3. Connect to (WINS-B), and set (WINS-A) as a push/pull replication partner of (WINS-B).
netsh wins server 192.168.0.189 add partner Server=192.168.125.30 Type=2

rem 4. Connect back to (WINS-A), and initiate a push replication to (WINS-B).
netsh wins server 192.168.125.30 init push Server=192.168.0.189 PropReq=0

rem 5. Connect to (WINS-B), and check that the record MY_RECORD [04h] was replicated successfully.
netsh wins server 192.168.0.189 show name Name=MY_RECORD EndChar=04

rem 6. End example batch file.
```

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>Команды netsh для WINS, используемые в примере пакетного файла

В следующем разделе перечислены команды **netsh для WINS**, которые используются в этом примере процедуры.

- **server**. Перемещает текущий контекст командной строки WINS на сервер, указанный по имени или IP-адресу.
- **add name**. Регистрирует имя на WINS-сервере.
- **add partner**. Добавляет партнера репликации для WINS-сервера.
- **init push**. Инициирует и отправляет триггер PUSH на WINS-сервер.
- **show name**. Отображает подробные сведения о конкретной записи в базе данных WINS-сервера.

## <a name="additional-references"></a>Дополнительная справка

- [Сетевая оболочка (Netsh)](netsh.md)
