---
title: tlntadmn
description: Справочная статья по команде tlntadmn, которая управляет локальным или удаленным компьютером, на котором запущена служба Telnet-сервера.
ms.topic: reference
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ee66352d2c5ee7787f6ee904b09bc3e929f019b8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805037"
---
# <a name="tlntadmn"></a>tlntadmn

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Управляет локальным или удаленным компьютером, на котором запущена служба Telnet-сервера. Если используется без параметров, то параметр **tlntadmn** отображает текущие параметры сервера.

Для этой команды требуется войти на локальный компьютер с учетными данными администратора. Для администрирования удаленного компьютера необходимо также указать учетные данные администратора для удаленного компьютера. Это можно сделать, войдя на локальный компьютер с учетной записью, имеющей административные учетные данные как для локального компьютера, так и для удаленного компьютера. Если этот метод использовать нельзя, можно использовать параметры **-u** и **-p** для предоставления учетных данных администратора удаленного компьютера.

## <a name="syntax"></a>Синтаксис

```
tlntadmn [<computername>] [-u <username>] [-p <password>] [{start | stop | pause | continue}] [-s {<sessionID> | all}] [-k {<sessionID> | all}] [-m {<sessionID> | all}  <message>] [config [dom = <domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <connections>] [port = <number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<computername>` | Указывает имя сервера для подключения. По умолчанию это локальный компьютер. |
| -u `<username> -p <password>` | Указывает учетные данные администратора для удаленного сервера, который требуется администрировать. Этот параметр является обязательным, если требуется администрировать удаленный сервер, к которому вы не выполнили вход с учетными данными администратора. |
| start | запускает службу Telnet Server. |
| stop | Останавливает службу сервера Telnet |
| pause | Приостанавливает работу службы Telnet Server. Новые подключения приниматься не будут. |
| continue | Возобновляет работу службы Telnet Server. |
| -s `{<sessionID> | all}` | Отображает активные сеансы Telnet. |
| -k `{<sessionID> | all}` | Завершает сеансы Telnet. Введите идентификатор сеанса, чтобы завершить конкретный сеанс, или введите ALL, чтобы завершить все сеансы. |
| -m `{<sessionID> | all}  <message>` | Отправляет сообщение в один или несколько сеансов. Введите идентификатор сеанса для отправки сообщения определенному сеансу или введите все, чтобы отправить сообщение всем сеансам. Введите сообщение, которое нужно отправить между кавычками. |
| Конфигурация DOM = `<domain>` | Настраивает домен по умолчанию для сервера. |
| Конфигурация ктрлакэймап = `{yes | no}` | Указывает, должен ли сервер Telnet интерпретировать сочетание клавиш CTRL + A как ALT. Введите **Да** , чтобы сопоставить сочетание клавиш, или введите " **нет** ", чтобы предотвратить сопоставление. |
| время ожидания конфигурации = `<hh>:<mm>:<ss>` | Задает интервал времени ожидания в часах, минутах и секундах. |
| Конфигурация тимеаутактиве = `{yes | no}` | Включает время ожидания бездействующего сеанса. |
| Конфигурация максфаил = `<attempts>` | Задает максимальное число неудачных попыток входа перед отключением. |
| Конфигурация максконн = `<connections>` | Задает максимальное число соединений. |
| Порт конфигурации = `<number>` | Задает порт Telnet. Необходимо указать порт с целым числом меньше 1024. |
| Конфигурация с `{+ | -}NTLM {+ | -}passwd` | Указывает, следует ли использовать NTLM, пароль или оба варианта для проверки подлинности при попытке входа. Чтобы использовать проверку подлинности определенного типа, введите знак плюс ( **+** ) перед этим типом проверки подлинности. Чтобы предотвратить использование определенного типа проверки подлинности, введите знак минус ( **-** ) перед этим типом проверки подлинности. |
| режим конфигурации = `{console | stream}` | Указывает режим работы. |
| -? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы настроить время ожидания бездействующего сеанса равным 30 минутам, введите:

```
tlntadmn config timeout=0:30:0
```

Чтобы отобразить активные сеансы Telnet, введите:

```
tlntadmn -s
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Руководство по операциям Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753164(v=ws.10))
