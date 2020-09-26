---
title: select volume
description: Справочная статья для команды Выбор тома, которая выбирает указанный том и перемещает фокус на него.
ms.topic: reference
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 643db6484842e8a67462b0460a1ecdeac653e577
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389192"
---
# <a name="select-volume"></a>select volume

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выбирает указанный том и перемещает фокус на него. Эта команда также может использоваться для показа тома, который в данный момент находится на выбранном диске.

## <a name="syntax"></a>Синтаксис

```
select volume={<n>|<d>}
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<n>` | Номер тома, получающего фокус. Вы можете просмотреть числа для всех томов на диске, выбранных в данный момент, с помощью команды " **список томов** " в DiskPart. |
| `<d> `| Буква диска или путь к точке подключения тома, получающего фокус. |

## <a name="remarks"></a>Комментарии

- Если том не указан, эта команда отображает том, на котором в данный момент находится фокус на выбранном диске.

- На базовом диске выбор тома также дает фокус соответствующему разделу.

  - Если выбран том с соответствующим разделом, раздел будет выбран автоматически.

  - Если секция выбрана с соответствующим томом, том будет выбран автоматически.

## <a name="examples"></a>Примеры

Чтобы переместить фокус на *том 2*, введите:

```
select volume=2
```

Чтобы переместить фокус на *диск C*, введите:

```
select volume=c
```

Чтобы переместить фокус на том, подключенный к папке с именем *к:\маунтпас*, введите:

```
select volume=c:\mountpath
```

Чтобы отобразить том, на котором в данный момент находится фокус на выбранном диске, введите:

```
select volume
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда "добавить том"](add-volume.md)

- [Команда "атрибуты тома"](attributes-volume.md)

- [Команда создания зеркального отображения тома](create-volume-mirror.md)

- [Команда создания тома RAID](create-volume-raid.md)

- [Команда создания простого тома](create-volume-simple.md)

- [Команда создания чередующихся томов](create-volume-stripe.md)

- [Команда "Удалить том"](delete-volume.md)

- [Команда "подробное описание тома"](detail-volume.md)

- [команда fsutil volume](fsutil-volume.md)

- [Команда "список томов"](list-volume.md)

- [Команда "автономный том"](offline-volume.md)

- [онине Volume, команда](online-volume.md)

- [Команда "выбрать диск"](select-disk.md)

- [Команда "выбрать секцию"](select-partition.md)

- [команда SELECT VDISK](select-vdisk.md)
