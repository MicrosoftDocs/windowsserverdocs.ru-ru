---
title: bootcfg rmsw
description: Справочная статья по команде bootcfg рмсв, которая удаляет параметры загрузки операционной системы для указанной записи операционной системы.
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ffe80c6a95421a66a1aebd119664c9e4f68952d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880543"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет параметры загрузки операционной системы для указанной записи операционной системы.

## <a name="syntax"></a>Синтаксис

```
bootcfg /rmsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `/s <computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте обратную косую черту). По умолчанию это локальный компьютер. |
| `/u <domain>\<user>`  | Выполняет команду с разрешениями учетной записи пользователя, указанного в параметре `<user>` или `<domain>\<user>` . По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| `/p <password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| /mm | Удаляет параметр/maxmem и связанное с ним максимальное значение памяти из указанного `<osentrylinenum>` . Параметр/maxmem указывает максимальный объем ОЗУ, который может использовать операционная система. |
| /bv | Удаляет параметр/басевидео из указанного `<osentrylinenum>` . Параметр/басевидео указывает операционной системе использовать стандартный режим VGA для установленного видеодрайвера. |
| /So | Удаляет параметр/SOS из указанного `<osentrylinenum>` . Параметр/SOS указывает операционной системе отображать имена драйверов устройств во время их загрузки. |
| /NG | Удаляет параметр/ногуибут из указанного `<osentrylinenum>` . Параметр/ногуибут отключает индикатор выполнения, который отображается перед запросом CTRL + ALT + DEL для входа. |
| `/id <osentrylinenum>` | Указывает номер строки записи операционной системы в разделе [Operating Systems] файла Boot.ini, в который добавляются параметры загрузки операционной системы. Первая строка после заголовка раздела [Operating Systems] — 1. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы использовать команду **bootcfg/rmsw** , выполните следующие действия.

```
bootcfg /rmsw /mm 64 /id 2
bootcfg /rmsw /so /id 3
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /rmsw /ng /id 2
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
