---
title: Импорт сценария DiskShadow
description: Справочная статья по команде Import, которая импортирует переносимую теневую копию из загруженного файла метаданных в систему.
ms.topic: reference
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e169acd0cc2904e0d9629567ad5a1cf19e60802e
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101816300"
---
# <a name="import-diskshadow"></a>Импорт (Diskshadow)

Импортирует переносимую теневую копию из загруженного файла метаданных в систему.

> СУЩЕСТВЕННО Перед использованием этой команды необходимо загрузить файл метаданных DiskShadow с помощью [команды загрузить метаданные](load-metadata.md) .

## <a name="syntax"></a>Синтаксис

```
import
```

#### <a name="remarks"></a>Remarks

- Перепереносимые теневые копии не сохраняются немедленно в системе. Их сведения хранятся в XML-файле документа компонентов резервного копирования, который DiskShadow автоматически запрашивает и сохраняет в файле метаданных. cab в рабочем каталоге. Используйте [команду Set Metadata](set-metadata.md) , чтобы изменить путь и имя этого XML-файла.

## <a name="examples"></a>Примеры

Ниже приведен пример скрипта DiskShadow, демонстрирующий использование команды **Import** :

```
#Sample DiskShadow script demonstrating IMPORT
SET CONTEXT PERSISTENT
SET CONTEXT TRANSPORTABLE
SET METADATA transHWshadow_p.cab
#P: is the volume supported by the Hardware Shadow Copy provider
ADD VOLUME P:
CREATE
END BACKUP
#The (transportable) shadow copy is not in the system yet.
#You can reset or exit now if you wish.

LOAD METADATA transHWshadow_p.cab
IMPORT
#The shadow copy will now be loaded into the system.
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Diskshadow, команда](diskshadow.md)