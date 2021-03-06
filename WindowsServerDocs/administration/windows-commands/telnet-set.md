---
title: telnet set
description: Справочная статья по команде Telnet Set, которая задает параметры.
ms.topic: reference
ms.assetid: 67316b5f-9c6f-43e3-86d5-dcff9ae2ac3e
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 33d0a51cb8d05ebab8c5c459075d3f488e3e8391
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805157"
---
# <a name="telnet-set"></a>Telnet: задать

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Задает параметры. Для выключения ранее установленного параметра можно использовать [команду Telnet](telnet-unset.md) unset.

## <a name="syntax"></a>Синтаксис

```
set [bsasdel] [crlf] [delasbs] [escape <char>] [localecho] [logfile <filename>] [logging] [mode {console | stream}] [ntlm] [term {ansi | vt100 | vt52 | vtnt}] [?]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| бсасдел | Отправляет **Backspace** в виде **удаления**. |
| CRLF | Отправляет CR & LF (0x0D, 0x 0A) при нажатии клавиши **Ввод** . Называется **режимом новой строки**. |
| деласбс | Отправляет **Удаление** в виде **Backspace**. |
| выполняет `<character>` | Задает escape-символ, используемый для ввода запроса клиента Telnet. Escape-символ может быть одиночным символом или сочетанием клавиши **CTRL** и символа. Чтобы задать сочетание клавиш управления, удерживайте нажатой клавишу **CTRL** при вводе символа, который требуется назначить. |
| локалечо | Включает локальный вывод. |
| logfile `<filename>` | Записывает текущий сеанс Telnet в локальный файл. Ведение журнала начинается автоматически при выборе этого параметра. |
| Ведение журнала | Включает ведение журнала. Если файл журнала не задан, выводится сообщение об ошибке. |
| режима `{console | stream}` | Задает режим работы. |
| NTLM | Включает проверку подлинности NTLM. |
| термин `{ansi | vt100 | vt52 | vtnt}` | Задает тип терминала. |
| ? | Отображает справку для этой команды. |

#### <a name="remarks"></a>Комментарии

- В версиях Telnet, отличных от английской, набор **кодов** `<option>` доступен. **Исходный код** `<option>` устанавливает для текущего кода значение, которое может быть любым из следующих: **SHIFT JIS**, **японская EUC**, **JIS**, кандзи, **JIS (78)**, **кандзи**( **NEC**), кандзи. Необходимо задать тот же набор кодов на удаленном компьютере.

## <a name="example"></a>Пример

Чтобы задать файл журнала и начать запись в локальный файл *tnlog.txt*, введите:

```
set logfile tnlog.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
