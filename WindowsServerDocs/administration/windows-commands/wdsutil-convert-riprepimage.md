---
title: Convert-Рипрепимаже
description: Справочная статья по Convert-Рипрепимаже, которая преобразует существующий образ подготовки удаленной установки (RIPrep) в формат образа Windows (WIM).
ms.topic: reference
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d9f29d4409389feb862278539105b10c54629bc9
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91731020"
---
# <a name="convert-riprepimage"></a>Convert-Рипрепимаже

Преобразует существующий образ подготовки удаленной установки (RIPrep) в формат образа Windows (WIM).

## <a name="syntax"></a>Синтаксис

```
WDSUTIL [Options] /Convert-RIPrepImage /FilePath:<File path and name>
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/InPlace]
         [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>Параметры

|            Параметр            |                                                                                                                                                                                                                                                                                                               Описание                                                                                                                                                                                                                                                                                                                |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Равно\<File path and name> |                                                                                                                                                                                                       Указывает полный путь и имя файла. sif, соответствующего образу RIPrep. Этот файл обычно называется RIPrep. sif и находится во вложенной папке \Темплатес папки, содержащей образ RIPrep.                                                                                                                                                                                                       |
|        /дестинатионимаже        | Задает параметры для конечного образа, используя следующие параметры.</br>-/FilePath.: \<File path and name> — задает полный путь к файлу для нового файла. Например: **к:\темп\конверт.Вим**</br>-[/Name: \<Name> ] — задает отображаемое имя образа. Если отображаемое имя не указано, будет использоваться отображаемое имя исходного изображения.</br>-[/Description: \<Description> ] — задает описание образа.</br>-[/Инплаце] — указывает, что преобразование должно осуществляться на исходном образе RIPrep, а не на копии исходного образа, что является поведением по умолчанию.</br>-[/Overwrite: {Да |

## <a name="examples"></a>Примеры

Чтобы преобразовать указанный образ RIPrep. sif в файл RIPREP. wim, введите:
```
WDSUTIL /Convert-RiPrepImage /FilePath:R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif /DestinationImage
/FilePath:C:\Temp\RIPREP.wim
```
Чтобы преобразовать указанный образ RIPrep. sif в файл RIPREP. wim с указанным именем и описанием и перезаписать его новым файлом, если он уже существует, введите:
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif
/DestinationImage /FilePath:\\Server\Share\RIPREP.wim
/Name:WindowsXP image /Description:Converted RIPREP image of WindowsXP
/Overwrite:Append
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)