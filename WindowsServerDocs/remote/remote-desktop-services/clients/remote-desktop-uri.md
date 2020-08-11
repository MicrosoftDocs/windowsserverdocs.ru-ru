---
title: Схема URI удаленного рабочего стола
description: Дополнительные сведения о схеме URI для клиентов удаленного рабочего стола
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 06/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: 082943114d00d9325e81edbd5cbeff14ba413703
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955091"
---
# <a name="remote-desktop-uri-scheme"></a>Схема URI удаленного рабочего стола

> Применяется к: Windows Server, версия 1803, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

В этом документе определяется формат универсальных кодов ресурсов (URI) для удаленного рабочего стола. Эти схемы URI позволяют вызывать клиенты удаленного рабочего стола с помощью разных команд.

## <a name="ms-rd-uri-scheme"></a>Схема URI ms-rd

>[!NOTE]
> В настоящее время схема URI ms-rd поддерживается только для клиента Рабочего стола Windows (MSRDC).

URI ms-rd предоставляет возможность указать для клиента команду и соответствующий набор параметров в следующем формате:

```
ms-rd:command?parameters
```

Эти параметры предоставляются в формате строк запроса, то есть в виде пар "ключ=значение" с разделителем &, и позволяют передать для команды дополнительные сведения:

```
param1=value1&param2=value2&…
```

### <a name="commands-and-parameters"></a>Команды и параметры

Ниже приведен список команд, которые поддерживаются в настоящее время, и параметров для них.

Использование `ms-rd:` без команд просто запускает клиент.

#### <a name="subscribe"></a>Subscribe

Эта команда запускает клиент и запускает процесс оформления подписки.

**Имя команды:** subscribe

**Параметры команды:**

| Параметр | Описание                  | Значения |
|-----------|------------------------------|--------|
| URL-адрес       | Указывает URL-адрес рабочего пространства. | Допустимый URL-адрес, например <https://contoso.com>. |

**Пример:** ms-rd:subscribe?url=https://contoso.com

## <a name="legacy-rdp-uri-scheme"></a>Старая схема URI для удаленного рабочего стола

>[!NOTE]
> Следующая схема URI поддерживается только в клиентах для устройств macOS, iOS и Android. Она постепенно заменяется новым форматом URI ms-rd, который описан выше.

Удаленный рабочий стол (Майкрософт) использует схему URI rdp://строка_запроса для хранения предварительно настроенных атрибутов, используемых при запуске клиента. Строки запросов представляют один атрибут или набор атрибутов RDP, указываемых в URL-адресе.

Атрибуты RDP разделяются символом амперсанда (&). Например, при подключении к ПК строка имеет следующий вид:

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

Эта таблица содержит полный список поддерживаемых атрибутов, которые могут использоваться с клиентами удаленных рабочих столов iOS, Mac и Android. (Символ x в столбце платформы означает, что атрибут поддерживается. Значения, обозначенные угловыми скобками (<>), представляют значения, поддерживаемые клиентами удаленного рабочего стола.)

| Атрибут протокола удаленного рабочего стола                                           | Android | Mac | iOS |
|---------------------------------------------------------|---------|-----|-----|
| allow desktop composition=i:&lt;0 или 1&gt;              | x       | x   | x   |
| allow font smoothing=i:<0 или 1&gt;                      | x       | x   | x   |
| alternate shell=s:&lt;строка&gt;                        | x       | x   | x   |
| [audiomode=i:&lt;0, 1 или 2&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393707(v=ws.10)) | x       | x   | x   |
| [authentication level=i:&lt;0 или 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393709(v=ws.10)) | x       | x   | x   |
| connect to console=i:&lt;0 или 1&gt;                     | x       | x   | x   |
| disable cursor settings=i:&lt;0 или 1&gt;                | x       | x   | x   |
| disable full window drag=i:&lt;0 или 1&gt;               | x       | x   | x   |
| disable menu anims=i:&lt;0 или 1&gt;                     | x       | x   | x   |
| disable themes=i:&lt;0 или 1&gt;                         | x       | x   | x   |
| disable wallpaper=i:&lt;0 или 1&gt;                      | x       | x   | x   |
| [drivestoredirect=s:*](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393728(v=ws.10)) (это единственное поддерживаемое значение) | x       | x   |     |
| [desktopheight=i:&lt;значение в пикселях&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393702(v=ws.10)) |         | x   |     |
| [desktopwidth=i:&lt;значение в пикселях&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393697(v=ws.10))  |         | x   |     |
| [domain=s:&lt;строка&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393673(v=ws.10))                 | x | x | x |
| [full address=s:&lt;строка&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393661(v=ws.10))           | x | x | x |
| gatewayhostname=s:&lt;строка&gt;                  | x | x | x |
| [gatewayusagemethod=i:&lt;1 или 2&gt;](/windows/win32/termserv/imsrdpclienttransportsettings-gatewayusagemethod)                | x | x | x |
| [prompt for credentials on client=i:&lt;0 или 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393660(v=ws.10)) |   | x |   |
| [loadbalanceinfo=s:&lt;строка&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393684(v=ws.10))                  | x | x | x |
| [redirectprinters=i:&lt;0 или 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393671(v=ws.10))                 |   | x |   |
| remoteapplicationcmdline=s:&lt;строка&gt;         | x | x | x |
| remoteapplicationmode=i:&lt;0 или 1&gt;            | x | x | x |
| remoteapplicationprogram=s:&lt;строка&gt;         | x | x | x |
| shell working directory=s:&lt;строка&gt;          | x | x | x |
| Use redirection server name=i:&lt;0 или 1&gt;      | x | x | x |
| [username=s:&lt;строка&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393678(v=ws.10))                  | x | x | x |
| [screen mode id=i:&lt;1 или 2&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393692(v=ws.10))            |   | x |   |
| [session bpp=i:&lt;8, 15, 16, 24 или 32&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393680(v=ws.10)) |   | x |   |
| [use multimon=i:&lt;0 или 1&gt;](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff393695(v=ws.10))              |   | x |   |
