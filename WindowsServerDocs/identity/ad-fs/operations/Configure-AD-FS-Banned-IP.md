---
title: Настройка AD FS запрещенных IP-адресов
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/28/2018
ms.topic: article
ms.openlocfilehash: e5cb939fcf862d16837c2f9e05548644faf3bf71
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956491"
---
# <a name="ad-fs-and-banned-ip-addresses"></a>AD FS и запрещенные IP-адреса


В июне 2018 AD FS на Windows Server 2016 предоставила **запрещенные IP-адреса** AD FS Июнь 2018.  Это обновление позволяет настроить набор IP-адресов глобально в AD FS, чтобы запросы, поступающие с этих IP-адресов, или IP-адреса из заголовков **x и** **MS-Forwarded-Client-IP** были заблокированы AD FS.

## <a name="adding-banned-ips"></a>Добавление запрещенных IP-адресов
Чтобы добавить запрещенные IP-адреса в глобальный список, используйте следующий командлет PowerShell:

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

Разрешенные форматы

1.  IPv4
2.  IPv6
3.  Формат CIDR с IPv4 или V6

Существует ограничение в 300 записей для запрещенных IP-адресов. Можно использовать CIDR или формат диапазона для запрета большого блока записей с одной записью.

## <a name="removing-banned-ips"></a>Удаление запрещенных IP-адресов
Чтобы удалить запрещенные IP-адреса из глобального списка, используйте следующий командлет PowerShell:

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>Чтение запрещенных IP-адресов
Чтобы прочитать текущий набор запрещенных IP-адресов, используйте следующий командлет PowerShell:

``` powershell
PS C:\ >Get-AdfsProperties
```

Выходные данные примера:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>Дополнительная справка
[Рекомендации по обеспечению безопасности службы федерации Active Directory (AD FS)](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-AdfsProperties](/powershell/module/adfs/set-adfsproperties?view=win10-ps)

[Операции AD FS](../ad-fs-operations.md)
