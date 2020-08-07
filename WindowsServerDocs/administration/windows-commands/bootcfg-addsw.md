---
title: bootcfg addsw
description: Справочная статья по команде bootcfg аддсв, которая добавляет параметры загрузки операционной системы для указанной записи операционной системы.
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 549bfec84cb45baec309d8ae7043be39f5d31a3a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880742"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет параметры загрузки операционной системы для указанной записи операционной системы.

## <a name="syntax"></a>Синтаксис

```
bootcfg /addsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm <maximumram>] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>Параметры

| Термин | Определение |
| ---- | ---------- |
| `/s <computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте обратную косую черту). По умолчанию это локальный компьютер. |
| `/u <domain>\<user>`  | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain>\<user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| `/p <password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| `/mm <maximumram>` | Указывает максимальный объем ОЗУ в мегабайтах, который может использоваться операционной системой. Значение должно быть больше или равно 32 МБ. |
| /bv | Добавляет параметр **/басевидео** к указанному `<osentrylinenum>` , который направляет операционную систему на использование стандартного режима VGA для установленного видеодрайвера. |
| /So | Добавляет в указанный параметр **/SOS** `<osentrylinenum>` , предоставляя операционной системе возможность отображать имена драйверов устройств во время их загрузки. |
| /NG | Добавляет параметр **/ногуибут** к указанному `<osentrylinenum>` , отключая индикатор выполнения, который отображается перед запросом Ctrl + Alt + Del для входа. |
| `/id <osentrylinenum>` | Указывает номер строки записи операционной системы в разделе [Operating Systems] файла Boot.ini, в который добавляются параметры загрузки операционной системы. Первая строка после заголовка раздела [Operating Systems] — 1. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы использовать команду **bootcfg/ADDSW** , выполните следующие действия.

```
bootcfg /addsw /mm 64 /id 2
bootcfg /addsw /so /id 3
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /addsw /ng /id 2
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
