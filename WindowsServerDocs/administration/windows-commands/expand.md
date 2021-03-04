---
title: expand
description: Справочная статья по команде Expand, которая расширяет один или несколько сжатых файлов.
ms.topic: reference
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2cada201982e90126783f7abd1a71ef60d71401e
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101818248"
---
# <a name="expand"></a>expand

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Развертывает один или несколько сжатых файлов. Эту команду также можно использовать для извлечения сжатых файлов с дисков распространения.

Команда **expand** также может запускаться из консоли восстановления Windows с использованием различных параметров. Дополнительные сведения см. в разделе [Среда восстановления Windows (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Синтаксис

```
expand [/r] <source> <destination>
expand /r <source> [<destination>]
expand /i <source> [<destination>]
expand /d <source>.cab [/f:<files>]
expand <source>.cab /f:<files> <destination>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /r | Переименовывает развернутые файлы. |
| source | Указывает файлы, которые нужно развернуть. *Источник* может состоять из буквы диска и двоеточия, имени каталога, имени файла или их сочетания. Можно использовать подстановочные знаки (**&#42;** или **?**). |
| ресурс destination | Указывает, где следует разворачивать файлы.<p>Если *источник* состоит из нескольких файлов и не указан параметр **/r**, *назначение* должно быть каталогом. *Назначение* может состоять из буквы диска и двоеточия, имени каталога, имени файла или их сочетания. `file | path`Спецификация назначения. |
| /i | Переименовывает развернутые файлы, но игнорирует структуру каталогов. |
| /d | Отображает список файлов в исходном расположении. Не расширяет или не извлекает файлы. |
| ключа`<files>` | Указывает файлы в CAB-файле, которые необходимо развернуть. Можно использовать подстановочные знаки (**&#42;** или **?**). |
| /? | Отображение справки в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
