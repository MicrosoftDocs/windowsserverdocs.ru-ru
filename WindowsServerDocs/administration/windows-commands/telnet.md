---
title: telnet
description: Справочная статья по команде Telnet, которая взаимодействует с компьютером, на котором работает служба Telnet-сервера.
ms.topic: reference
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4ff06070dcfc291376a78195d3825254b380d11d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805137"
---
# <a name="telnet"></a>telnet

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Взаимодействует с компьютером, на котором запущена служба Telnet-сервера. Выполнение этой команды без параметров позволяет ввести контекст Telnet, как указано в командной строке Telnet (**Microsoft telnet>**). В командной строке Telnet можно использовать команды Telnet для управления компьютером, на котором выполняется клиент Telnet.

> [!IMPORTANT]
> Для выполнения этой команды необходимо установить клиентское программное обеспечение Telnet. Дополнительные сведения см. в разделе [Установка Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10)).

## <a name="syntax"></a>Синтаксис

```
telnet [/a] [/e <escapechar>] [/f <filename>] [/l <username>] [/t {vt100 | vt52 | ansi | vtnt}] [<host> [<port>]] [/?]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /a | Предпринимает попытку автоматического входа. То же, что и параметр **/l** , за исключением того, что он использует имя текущего вошедшего в систему пользователя. |
| /e `<escapechar>` | Указывает escape-символ, используемый для ввода запроса клиента Telnet. |
| /f `<filename>` | Указывает имя файла, используемого для ведения журнала на стороне клиента. |
| /l `<username>` | Указывает имя пользователя для входа на удаленный компьютер. |
| /t `{vt100 | vt52 | ansi | vtnt}` | Указывает тип терминала. Поддерживаются следующие типы терминалов: **VT100**, **VT52**, **ANSI** и **VTNT**. |
| `<host> [<port>]` | Указывает имя узла или IP-адрес удаленного компьютера, к которому необходимо подключиться, и при необходимости используемый TCP-порт (по умолчанию это TCP-порт 23). |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы использовать Telnet для подключения к компьютеру, на котором запущена служба сервера Telnet по адресу *Telnet.Microsoft.com*, введите:

```
telnet telnet.microsoft.com
```

Чтобы использовать Telnet для подключения к компьютеру, на котором запущена служба Telnet-сервера по адресу *Telnet.Microsoft.com на TCP-порте 44* и ro журнал активности сеанса в локальном файле с именем *telnetlog.txt*, введите:

```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Установка Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10))

- [Технический справочник по Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754987(v=ws.10))
