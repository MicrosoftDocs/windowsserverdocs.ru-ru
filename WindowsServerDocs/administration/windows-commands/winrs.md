---
title: winrs
description: Справочная статья по WinRS, позволяющее удаленно управлять программами и выполнять их.
ms.topic: reference
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 91a57e517a6b177c1a095ed1748a3043441aa08a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826692"
---
# <a name="winrs"></a>winrs

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаленное управление Windows позволяет удаленно управлять и выполнять программы.
## <a name="syntax"></a>Синтаксис
```
winrs [/<parameter>[:<value>]] <command>
```
#### <a name="parameters"></a>Параметры

|           Параметр            |                                                                                                                                                                                    Описание                                                                                                                                                                                     |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      удаленный\<endpoint>       |                                                                                          Указывает целевую конечную точку, используя NetBIOS-имя или стандартное подключение:<p>-   <url>: [\<transport>://]\<target>[:\<port>]<p>Если не указано, используется **/r: localhost** .                                                                                          |
|          /уненкриптед          | Указывает, что сообщения удаленной оболочки не будут зашифрованы. Это полезно для устранения неполадок или в случае, когда сетевой трафик уже зашифрован с помощью **IPSec** или когда применяется физическая безопасность.<p>По умолчанию сообщения шифруются с помощью ключей Kerberos или NTLM.<p>Этот параметр командной строки игнорируется, если выбран транспорт HTTPS. |
|     /username\<username>      |                                                                                Указывает имя пользователя в командной строке.<p>Если этот параметр не указан, средство будет использовать проверку подлинности Negotiate или запросить имя.<p>Если указан **/username** , необходимо также указать **/Password** .                                                                                 |
|     /Password\<password>      |                                                                           Задает пароль для командной строки.<p>Если параметр **/Password** не указан, но **/username** имеет значение, средство запросит пароль.<p>Если указан **/Password** , необходимо также указать **/username** .                                                                            |
|      /timeout\<seconds>       |                                                                                                                                                                             Этот параметр использовать не рекомендуется.                                                                                                                                                                             |
|       /Directory\<path>       |                                                                                            Указывает начальный каталог для удаленной оболочки.<p>Если этот параметр не указан, удаленная оболочка будет запускаться в домашнем каталоге пользователя, определенном переменной среды **% UserProfile%**.                                                                                             |
| PXE\<string>=<value> |                                                                          Задает одну переменную среды, которая должна быть задана при запуске оболочки, что позволяет изменять среду по умолчанию для оболочки.<p>Для указания нескольких переменных среды необходимо использовать несколько экземпляров этого переключателя.                                                                          |
|            /ноечо             |                                                                                                    Указывает, что вывод должен быть отключен. Это может потребоваться, чтобы убедиться, что ответы пользователя на удаленные запросы не отображаются локально.<p>По умолчанию включен режим Echo.                                                                                                    |
|           /нопрофиле           |                                              Указывает, что профиль пользователя не должен загружаться.<p>По умолчанию сервер попытается загрузить профиль пользователя.<p>Если удаленный пользователь не является локальным администратором в целевой системе, этот параметр будет необходим (по умолчанию это приведет к ошибке).                                               |
|         /алловделегате         |                                                                                                                  Указывает, что учетные данные пользователя можно использовать для доступа к удаленной общей папке, например, на компьютере, отличном от компьютера целевой конечной точки.                                                                                                                   |
|          /Compression          |                                                                           Включите сжатие.  Более старые установки на удаленных компьютерах могут не поддерживать сжатие, поэтому по умолчанию отключено.<p>Значение по умолчанию — OFF, так как старые установки на удаленных компьютерах могут не поддерживать сжатие.                                                                           |
|            /усессл             |                                                                                                               Используйте SSL-соединение при использовании удаленной конечной точки.  Указание этого параметра вместо транспорта **https:** будет использовать порт по умолчанию для **WinRM** по умолчанию.                                                                                                                |
|               /?               |                                                                                                                                                                        Отображение справки в командной строке.                                                                                                                                                                        |

## <a name="remarks"></a>Комментарии
-   Все параметры командной строки принимают либо краткую форму, либо длинную форму. Например, допустимыми являются **/r** и **/ремоте** .
-   Чтобы завершить команду **/ремоте** , пользователь может ввести **сочетание клавиш CTRL-C** или **Ctrl-Break**, которое будет отправлено удаленной оболочке. Вторая **клавиша CTRL-C** принудительно завершает **winrs.exe**.
-   Для управления активными удаленными оболочками или конфигурацией WinRS используйте средство WinRM.  Псевдоним универсального кода ресурса (URI) для управления активными оболочками — **Shell/cmd**.  Псевдоним URI для конфигурации WinRS — **WinRM/config/WinRS**.

## <a name="examples"></a>Примеры
```
winrs /r:https://contoso.com command
```
```
winrs /r:contoso.com /usessl command
```
```
winrs /r:myserver command
```
```
winrs /r:http://127.0.0.1 command
```
```
winrs /r:http://169.51.2.101:80 /unencrypted command
```
```
winrs /r:https://[::FFFF:129.144.52.38] command
```
```
winrs /r:http://[1080:0:0:0:8:800:200C:417A]:80 command
```
```
winrs /r:https://contoso.com /t:600 /u:administrator /p:$%fgh7 ipconfig
```
```
winrs /r:myserver /env:path=^%path^%;c:\tools /env:TEMP=d:\temp config.cmd
```
```
winrs /r:myserver netdom join myserver /domain:testdomain /userd:johns /passwordd:$%fgh789
```
```
winrs /r:myserver /ad /u:administrator /p:$%fgh7 dir \\anotherserver\share
```

## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

