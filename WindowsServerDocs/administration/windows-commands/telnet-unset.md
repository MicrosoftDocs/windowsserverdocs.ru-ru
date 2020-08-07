---
title: telnet unset
description: Справочная статья для Telnet без параметров, которая отключает ранее установленные параметры.
ms.topic: article
ms.assetid: da9a0d99-1930-4858-93c7-0e9c3797ee09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e90c6696ec4dd2883d4627862c4ad2db638b1c6e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881637"
---
# <a name="telnet-unset"></a>Telnet: не задано

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отключает ранее установленные параметры.

## <a name="syntax"></a>Синтаксис
```
u[nset] {bsasdel | crlf | delasbs | escape | localecho | logging | ntlm} [?]
```
#### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|бсасдел|Отправляет **Backspace** в виде **Backspace**.|
|CRLF|Отправляет клавишу **Ввод** в виде CR. Также называется режимом перевода строки.|
|деласбс|Отправляет **Удаление** как **Удаление**.|
|escape-знак|Удаляет параметр escape-символа.|
|локалечо|Отключает локалечо.|
|Ведение журналов|Отключает ведение журнала.|
|NTLM|Отключает проверку подлинности NTLM.|
|?|Отображает справку для этой команды.|
## <a name="examples"></a>Примеры
Отключите ведение журнала.
```
u logging
```
## <a name="additional-references"></a>Дополнительные ссылки
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
