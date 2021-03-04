---
title: pubprn
description: Справочная статья по команде Pubprn, которая публикует принтер в службах домен Active Directory.
ms.topic: reference
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e74a91a566286a7a44a0de0fced67e16f909b608
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101807873"
---
# <a name="pubprn"></a>pubprn

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Публикует принтер в службах домен Active Directory. Эта команда представляет собой Visual Basic сценарий, расположенный в `%WINdir%\System32\printing_Admin_Scripts\<language>` каталоге. Чтобы использовать эту команду в командной строке, введите **cscript** , а затем полный путь к файлу Pubprn или измените каталоги на соответствующую папку. Например: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn`.

## <a name="syntax"></a>Синтаксис

```
cscript pubprn {<servername> | <UNCprinterpath>} LDAP://CN=<container>,DC=<container>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<servername>` | Указывает имя сервера Windows, на котором размещен принтер, который требуется опубликовать. Если компьютер не указан, используется локальный компьютер. |
| `<UNCprinterpath>` | UNC-путь к общему принтеру, который требуется опубликовать. |
| `LDAP://CN=<Container>,DC=<Container>` | Указывает путь к контейнеру в службах домен Active Directory Services, где требуется опубликовать принтер. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Если предоставленные сведения содержат пробелы, заключите его в кавычки (например, "имя компьютера").

### <a name="examples"></a>Примеры

Чтобы опубликовать все принтеры на \\ компьютере Server1 в контейнере MyContainer в домене mydomain.Company.com, введите:

```
cscript pubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

Чтобы опубликовать принтер Laserprinter1 на \\ сервере \Server1 в контейнер MyContainer в домене mydomain.Company.com, введите:

```
cscript pubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам системы печати](print-command-reference.md)
