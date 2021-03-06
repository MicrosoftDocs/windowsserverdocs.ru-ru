---
title: regini
description: Справочная статья по команде Регини, которая изменяет реестр из командной строки или сценария и применяет изменения, предустановленные в одном или нескольких текстовых файлах.
ms.topic: reference
ms.assetid: 5ff18dc3-5bd8-400a-b311-fd73a3267e8c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 1a3878f4941a44a8c51ec2fd82dade1b9dd61a24
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101807177"
---
# <a name="regini"></a>regini

Изменяет реестр из командной строки или сценария и применяет изменения, предустановленные в одном или нескольких текстовых файлах. Вы можете создавать, изменять и удалять разделы реестра, а также изменять разрешения для разделов реестра.

Дополнительные сведения о формате и содержимом текстового файла скрипта, который regini.exe использует для внесения изменений в реестр, см. в разделе [изменение значений или разрешений реестра из командной строки или сценария](https://support.microsoft.com/help/264584/how-to-change-registry-values-or-permissions-from-a-command-line-or-a).

## <a name="syntax"></a>Синтаксис

```
regini [-m \\machinename | -h hivefile hiveroot][-i n] [-o outputwidth][-b] textfiles...
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -m `<\\computername>` | Указывает имя удаленного компьютера с изменяемым реестром. Используйте формат **\\ ComputerName**. |
| -h `<hivefile hiveroot>` | Указывает куст локального реестра для изменения. Необходимо указать имя файла Hive и корневой каталог Hive в формате **хивефиле хиверут**. |
| -i `<n>` | Задает уровень отступа, используемый для указания древовидной структуры разделов реестра в выходных данных команды. Средство **regdmp.exe** (которое получает текущие разрешения раздела реестра в двоичном формате) использует отступы, кратные четырем, поэтому значение по умолчанию — **4**. |
| -o `<outputwidth>` | Задает ширину выходных данных команды в символах. Если выходные данные будут отображаться в окне команд, значением по умолчанию будет ширина окна. Если выходные данные направляются в файл, значение по умолчанию — **240** символов. |
| -b | Указывает, что **regini.exe** выходные данные обратно совместимы с предыдущими версиями **regini.exe**. |
| Textfiles | Указывает имя одного или нескольких текстовых файлов, содержащих данные реестра. В списке можно указать любое количество текстовых файлов в кодировке ANSI или Unicode. |

#### <a name="remarks"></a>Комментарии

Следующие рекомендации применяются в основном к содержимому текстовых файлов, содержащих данные реестра, которые применяются с помощью **regini.exe**.

- Используйте точку с запятой как символ комментария в конце строки. Он должен быть первым непустым символом в строке.

- Используйте обратную косую черту, чтобы указать продолжение строки. Команда будет игнорировать все символы обратной косой черты до (но не включая) первого непустого символа следующей строки. Если перед обратной косой чертой указано более одного пробела, оно заменяется одним пробелом.

- Используйте символы жесткого табуляции для управления отступами. Этот отступ указывает древовидную структуру разделов реестра. Однако эти символы преобразуются в один пробел, независимо от их расположения.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
