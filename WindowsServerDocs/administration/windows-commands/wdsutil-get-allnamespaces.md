---
title: WDSUTIL Get-аллнамеспацес
description: Справочная статья по WDSUTIL Get-аллнамеспацес, в которой отображаются сведения обо всех пространствах имен на сервере.
ms.topic: reference
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f56ba5c1eaae6b4d428aa5d78d8b1f8fd16f91ae
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825891"
---
# <a name="wdsutil-get-allnamespaces"></a>WDSUTIL Get-аллнамеспацес

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает сведения обо всех пространствах имен на сервере.

## <a name="syntax"></a>Синтаксис
Для Windows Server 2008.
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/Show:Clients] [/ExcludedeletePending]
```
Приложение.
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/details:Clients] [/ExcludedeletePending]
```
### <a name="parameters"></a>Параметры

|         Параметр         |                                                                               Windows Server 2008                                                                               | Windows Server 2008 R2 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|  [/Server: <Server name> ]  | Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер. |                        |
| [/Контентпровидер: <name> ] |                                                        Отображает пространства имен только для указанного поставщика содержимого.                                                         |                        |
|      [/Show: Clients]      |                            Поддерживается только для Windows Server 2008. Отображает сведения о клиентских компьютерах, подключенных к пространству имен.                             |                        |
|    [/детаилс: клиенты]     |                           Поддерживается только для Windows Server 2008 R2. Отображает сведения о клиентских компьютерах, подключенных к пространству имен.                           |                        |
|  [/Ексклудеделетепендинг]  |                                                              Исключает из списка все деактивированные передачи.                                                              |                        |

## <a name="examples"></a>Примеры
Чтобы просмотреть все пространства имен, введите:
```
wdsutil /Get-AllNamespaces
```
Чтобы просмотреть все пространства имен, кроме отключенных, введите:
- Windows Server 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /details:Clients /ExcludedeletePending
  ```

## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
- [Команда WDSUTIL New-Namespace](wdsutil-new-namespace.md)
- [Команда WDSUTIL Remove-Namespace](wdsutil-remove-namespace.md)
- [Команда WDSUTIL Start-нмеспаце](wdsutil-start-namespace.md)
