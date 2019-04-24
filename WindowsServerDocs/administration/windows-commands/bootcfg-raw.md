---
title: bootcfg raw
description: Раздел Windows команды для **bootcfg необработанные** -добавляет параметры загрузки операционной системы, указанное в виде строки для записи операционной системы в **[операционные системы]** раздел файла Boot.ini.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a68c59eb3a7018ba8a7c0c96b594f0ed68d914b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841605"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавление параметров загрузки операционной системы, указанное в виде строки для записи операционной системы в **[операционные системы]** раздел файла Boot.ini.

## <a name="syntax"></a>Синтаксис
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
## <a name="parameters"></a>Параметры
|Термин|Определение|
|----|-------|
|/s <computer>|Указывает имя или IP-адрес удаленного компьютера (не используйте символы обратной косой черты). По умолчанию используется локальный компьютер.|
|/u <Domain> \\<User>|Выполняет команду с разрешениями учетной записи пользователя, указанного по <User> или <Domain> \\ <User>. По умолчанию используется разрешения текущего, вошедшего в систему пользователя на компьютере, используя следующую команду.|
|/p <Password>|Указывает пароль для учетной записи пользователя, который указан в **/u** параметра.|
|<OSLoadOptionsString>|Указывает параметры загрузки операционной системы, чтобы добавить запись операционной системы. Эти параметры загрузки заменяют все существующие параметры загрузки, связанные с записью в операционной системе. Проверка <OSLoadOptions> выполняется.|
|/ID <OSEntryLineNum>|Указывает номер строки записи операционной системы в разделе [operating systems] файла Boot.ini, для обновления. Первая строка после заголовка раздела [операционные системы]-1.|
|/a|Указывает, что добавляемый параметры операционной системы должна добавляться к все существующие параметры операционной системы.|
|/?|Отображение справки в командной строке.|
##### <a name="remarks"></a>Примечания
-   **необработанные bootcfg** используется для добавления текста в конец записи операционной системы, перезаписывая все существующие параметры записи операционной системы. Этот текст должен содержать допустимые параметры загрузки операционной системы, такие как **/debug**, **/fastdetect**, **/nodebug**, **/baudrate**, **/ crashdebug**, и **/SOS**. Например, следующая команда добавляет "**/debug/fastdetect**" в конец первой записи операционной системы, заменив все предыдущие параметры записи операционной системы:
    ```
    bootcfg /raw "/debug /fastdetect" /id 1
    ```
## <a name="BKMK_examples"></a>Примеры
В следующих примерах показано, как можно использовать **bootcfg / необработанные** команды:
```
bootcfg /raw "/debug /sos" /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 "/crashdebug " /id 2
```
#### <a name="additional-references"></a>Дополнительные ссылки
[Ключ синтаксиса командной строки](command-line-syntax-key.md)