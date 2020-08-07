---
title: Get-Аллнамеспацес
description: Справочная статья по команде Get-Аллнамеспацес, в которой отображаются сведения обо всех пространствах имен на сервере.
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 470aab904f9404b8dbe99409445b0533fa83fedd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896394"
---
# <a name="get-allnamespaces"></a>Get-Аллнамеспацес

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

|         Параметр         |                                                                               Windows Server 2008                                                                               | Windows Server 2008 R2 |
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
- Windows Server 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /details:Clients /ExcludedeletePending
  ```
  ## <a name="additional-references"></a>Дополнительные ссылки
  - Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
   [Использование команды](using-the-new-namespace-command.md) 
   New-Namespace [Использование команды](using-the-remove-namespace-command.md) 
   Remove-Namespace [Подкоманда: Start-Namespace](subcommand-start-namespace.md)
