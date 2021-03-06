---
title: gpfixup
description: Справочная статья по команде гпфиксуп, которая устраняет зависимости имен доменов в групповая политика объектах и групповая политика ссылки после операции переименования домена.
ms.topic: reference
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 14c4231c6caa05e4a5490e34bf17181cc49ab9d3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101816850"
---
# <a name="gpfixup"></a>gpfixup

Устраняет зависимости имен доменов в групповая политика объектах и ссылки групповая политика после операции переименования домена. Чтобы использовать эту команду, необходимо установить групповая политика Management в качестве компонента с помощью диспетчер сервера.

## <a name="syntax"></a>Синтаксис

```
gpfixup [/v]
[/olddns:<olddnsname> /newdns:<newdnsname>]
[/oldnb:<oldflatname> /newnb:<newflatname>]
[/dc:<dcname>] [/sionly]
[/user:<username> [/pwd:{<password>|*}]] [/?]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- |------------ |
| /v | Отображает подробные сообщения о состоянии. Если этот параметр не используется, отображается только сообщение об ошибке или сводка по состоянию на уведомление, **успешное** или **неуспешное** выполнение. |
| /олдднс:`<olddnsname>` | Указывает старое DNS-имя переименованного домена, как `<olddnsname>` если бы операция переименования домена изменила DNS-имя домена. Этот параметр можно использовать, только если вы также используете параметр **/невднс** для указания нового DNS-имени домена. |
| /невднс:`<newdnsname>` | Указывает новое DNS-имя переименованного домена, как `<newdnsname>` если бы операция переименования домена изменила DNS-имя домена. Этот параметр можно использовать, только если вы также используете параметр **/олдднс** , чтобы указать старое DNS-имя домена. |
| /олднб:`<oldflatname>` | Указывает старое NetBIOS-имя переименованного домена, как `<oldflatname>` если бы операция переименования домена изменила NetBIOS-имя домена. Этот параметр можно использовать только в том случае, если для указания нового NetBIOS-имени домена используется параметр **/невнб** . |
| /невнб:`<newflatname>` | Указывает новое NetBIOS-имя переименованного домена, как `<newflatname>` если бы операция переименования домена изменила имя NetBIOS домена. Этот параметр можно использовать, только если вы используете параметр **/олднб** , чтобы указать старое NetBIOS-имя домена. |
| /DC`<dcname>` | Подключитесь к контроллеру домена с именем `<dcname>` (DNS-имя или NetBIOS-имя). `<dcname>` необходимо разместить записываемую реплику раздела каталога домена, как показано в одном из следующих:<ul><li>DNS-имя с `<newdnsname>` помощью **/невднс**</li><li>Имя NetBIOS с `<newflatname>` помощью **/невнб**</br>Если этот параметр не используется, можно подключиться к любому контроллеру домена в переименованном домене, указанном параметром `<newdnsname>` или `<newflatname>` .</li></ul> |
| /сионли | Выполняет только групповая политика исправление, связанное с установкой управляемого программного обеспечения (расширение установки программного обеспечения для групповая политика). Пропустите действия, которые исправляют групповая политика ссылки и пути SYSVOL в объектах групповой политики. |
| WMIC`<username>` |Выполняет эту команду в контексте безопасности пользователя `<username>` , где `<username>` имеет формат домен \ пользователь. Если этот параметр не используется, эта команда выполняется от имени пользователя, выполнившего вход. |
| /PWD`{<password> | *}` | Указывает пароль для пользователя. |
| /? | Отображает справку в командной строке. |

### <a name="examples"></a>Примеры

В этом примере предполагается, что вы уже выполнили операцию переименования домена, в которой имя DNS изменено с **мйолдднснаме** на **Миневднснаме**, а NetBIOS-имя — с **мйолднетбиоснаме** на **миневнетбиоснаме**.

В этом примере команда **гпфиксуп** используется для подключения к контроллеру домена с именем **Мидкднснаме** и восстановления объектов групповой политики и групповая политика ссылок путем обновления старого доменного имени, внедренного в объекты групповой политики и ссылки. Состояние и вывод ошибок сохраняются в файл с именем **гпфиксуп. log**.

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

Этот пример аналогичен предыдущему, но предполагает, что NetBIOS-имя домена не было изменено во время операции переименования домена.

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Администрирование домен Active Directory переименование](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794869(v=ws.10))
