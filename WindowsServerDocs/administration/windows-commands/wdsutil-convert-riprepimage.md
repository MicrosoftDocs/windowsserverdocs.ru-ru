---
title: Convert-рипрепимаже
description: Справочная статья по команде Convert-рипрепимаже, которая преобразует существующий образ подготовки удаленной установки (RIPrep) в формат образа Windows (WIM).
ms.topic: reference
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 98b9b5d2543fd95a9ebfbbc9bc742e40d5600530
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804017"
---
# <a name="convert-riprepimage"></a>Convert-рипрепимаже

Преобразует существующий образ подготовки удаленной установки (RIPrep) в формат образа Windows (WIM).

## <a name="syntax"></a>Синтаксис

```
wdsutil [Options] /Convert-RIPrepImage /FilePath:<Filepath and name> /DestinationImage /FilePath:<Filepath and name> [/Name:<Name>] [/Description:<Description>] [/InPlace] [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Равно`<Filepath and name>` | Указывает полный путь к файлу и имя файла. sif, соответствующие образу RIPrep. Этот файл обычно называется RIPrep. sif и находится во вложенной папке **\темплатес** папки, содержащей образ RIPrep. |
| /дестинатионимаже | Задает параметры для конечного образа.  Использует следующие параметры.<ul><li>`/FilePath:<Filepath and name>` — Задает полный путь к файлу для нового файла. Например: **к:\темп\конверт.Вим**</li><li>[ `/Name:<Name>` ] — Задает отображаемое имя образа. Если отображаемое имя не указано, используется отображаемое имя исходного изображения.</li><li>[ `/Description:<Description>` ] — Задает описание образа.</li><li>[/Инплаце] — указывает, что преобразование должно осуществляться на исходном образе RIPrep, а не на копии исходного образа, что является поведением по умолчанию.</li><li>[ `/Overwrite:{Yes | No | Append}` -Указывает, будет ли этот образ перезаписывать или добавлять существующие файлы.</li></ul> |

## <a name="examples"></a>Примеры

Чтобы преобразовать указанный образ RIPrep. sif в файл RIPREP. wim, введите:

```
wdsutil /Convert-RiPrepImage /FilePath:R:\RemoteInstall\Setup\English \Images\Win2k3.SP1\i386\Templates\riprep.sif /DestinationImage /FilePath:C:\Temp\RIPREP.wim
```

Чтобы преобразовать указанный образ RIPrep. sif в файл RIPREP. wim с указанным именем и описанием и перезаписать его новым файлом, если он уже существует, введите:

```
wdsutil /Verbose /Progress /Convert-RiPrepImage /FilePath:\\Server \RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif /DestinationImage /FilePath:\\Server\Share\RIPREP.wim /Name:WindowsXP image /Description:Converted RIPREP image of WindowsXP /Overwrite:Append
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Командлеты служб развертывания Windows](/powershell/module/wds)
