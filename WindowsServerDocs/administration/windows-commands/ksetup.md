---
title: ksetup
description: Справочная статья по команде ksetup, которая выполняет задачи, связанные с настройкой и обслуживанием протокола Kerberos и центр распространения ключей (KDC) для поддержки сфер Kerberos.
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fc51f90f553ea2478c0c8f78cf77f7373eb47d7f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887676"
---
# <a name="ksetup"></a>ksetup

Выполняет задачи, связанные с настройкой и обслуживанием протокола Kerberos и центр распространения ключей (KDC) для поддержки сфер Kerberos. В частности, эта команда используется в следующих случаях:

- Измените параметры компьютера для обнаружения сфер Kerberos. В реализациях, основанных не на базе протокола Kerberos, эта информация обычно хранится в файле krb5. conf. В операционных системах Windows Server она хранится в реестре. Это средство можно использовать для изменения этих параметров. Эти параметры используются рабочими станциями для нахождение сфер Kerberos и контроллеров домена для нахождение сфер Kerberos для отношений доверия между сферами.

- Инициализируйте разделы реестра, используемые поставщиком поддержки безопасности Kerberos (SSP) для определения местонахождения центра распространения ключей для области Kerberos, если компьютер не является членом домена Windows. После настройки пользователь клиентского компьютера под управлением операционной системы Windows может войти в учетную запись в области Kerberos.

- Найдите в реестре доменное имя области пользователя, а затем разрешите имя по IP-адресу, запросив DNS-сервер. Протокол Kerberos может использовать DNS для определения Кдкс только с именем области, но для этого он должен быть специально настроен.

## <a name="syntax"></a>Синтаксис

```
ksetup
[/setrealm <DNSdomainname>]
[/mapuser <principal> <account>]
[/addkdc <realmname> <KDCname>]
[/delkdc <realmname> <KDCname>]
[/addkpasswd <realmname> <KDCPasswordName>]
[/delkpasswd <realmname> <KDCPasswordName>]
[/server <servername>]
[/setcomputerpassword <password>]
[/removerealm <realmname>]
[/domain <domainname>]
[/changepassword <oldpassword> <newpassword>]
[/listrealmflags]
[/setrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/dumpstate]
[/addhosttorealmmap] <hostname> <realmname>]
[/delhosttorealmmap] <hostname> <realmname>]
[/setenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <domainname>
[/addenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <domainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| [ksetup setrealm](ksetup-setrealm.md) | Делает этот компьютер членом области Kerberos. |
| [ksetup addkdc](ksetup-addkdc.md) | Определяет запись KDC для данной области. |
| [ksetup delkdc](ksetup-delkdc.md) | Удаляет запись KDC для области. |
| [ksetup addkpasswd](ksetup-addkpasswd.md) | Добавляет адрес сервера кпассвд для области. |
| [ksetup delkpasswd](ksetup-delkpasswd.md) | Удаляет адрес сервера кпассвд для области. |
| [ksetup server](ksetup-server.md) | Позволяет указать имя компьютера Windows, на котором будут применяться изменения. |
| [ksetup setcomputerpassword](ksetup-setcomputerpassword.md) | Задает пароль для учетной записи домена компьютера (или субъекта-узла). |
| [ksetup removerealm](ksetup-removerealm.md) | Удаляет из реестра все сведения для указанной области. |
| [ksetup domain](ksetup-domain.md) | Позволяет указать домен (если он еще `<domainname>` не был задан параметром **/domain** ). |
| [ksetup changepassword](ksetup-changepassword.md) | Позволяет использовать кпассвд для изменения пароля пользователя, вошедшего в систему. |
| [ksetup listrealmflags](ksetup-listrealmflags.md) | Список доступных флагов области, которые **ksetup** может обнаружить. |
| [ksetup setrealmflags](ksetup-setrealmflags.md) | Задает флаги области для определенной области. |
| [ksetup addrealmflags](ksetup-addrealmflags.md) | Добавляет дополнительные флаги сферы в область. |
| [ksetup delrealmflags](ksetup-delrealmflags.md) | Удаляет флаги сферы из области. |
| [ksetup dumpstate](ksetup-dumpstate.md) | Анализирует конфигурацию Kerberos на данном компьютере. Добавляет в реестр сопоставление узла с областью. |
| [ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md) | Добавляет значение реестра для отображения узла в области Kerberos. |
| [ksetup delhosttorealmmap](ksetup-delhosttorealmmap.md) | Удаляет значение реестра, которое сопоставляет главный компьютер с областью Kerberos. |
| [ksetup setenctypeattr](ksetup-setenctypeattr.md) | Задает один или несколько типов шифрования для атрибутов доверия для домена. |
| [ksetup getenctypeattr](ksetup-getenctypeattr.md) | Возвращает атрибут доверия типов шифрования для домена. |
| [ksetup addenctypeattr](ksetup-addenctypeattr.md) | Добавляет типы шифрования в атрибут Trust типов шифрования для домена. |
| [ksetup delenctypeattr](ksetup-delenctypeattr.md) | Удаляет атрибут доверия типов шифрования для домена. |
| /? | Отображает справку в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)