---
title: select partition
description: Справочная статья для команды выбор Секции, которая выбирает указанную секцию и перемещает фокус на нее.
ms.topic: reference
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 081c35bf96e99872d3699b120d38785362bd514b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806107"
---
# <a name="select-partition"></a>select partition

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выбирает указанную секцию и перемещает фокус на нее. Эта команда также может использоваться для вывода раздела, который в данный момент находится на выбранном диске.

## <a name="syntax"></a>Синтаксис

```
select partition=<n>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Секция =`<n>` | Номер секции, получающей фокус. Числа для всех разделов на диске, выбранных в данный момент, можно просмотреть с помощью команды **list partition** в DiskPart. |

#### <a name="remarks"></a>Комментарии

- Перед тем как выбрать раздел, необходимо сначала выбрать диск с помощью команды **Выбор диска** .

  - Если номер секции не указан, этот параметр отображает раздел, на котором в данный момент находится фокус на выбранном диске.

  - Если выбран том с соответствующим разделом, автоматически выбирается секция.

  - Если секция выбрана с соответствующим томом, том будет выбран автоматически.

## <a name="examples"></a>Примеры

Чтобы переместить фокус на *раздел 3*, введите:

```
select partitition=3
```

Чтобы отобразить раздел, который в данный момент находится на выбранном диске, введите:

```
select partition
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда "создать секцию EFI"](create-partition-efi.md)

- [Создание расширенной команды Partition](create-partition-extended.md)

- [Создание логической команды секции](create-partition-logical.md)

- [Команда создания секции MSR](create-partition-msr.md)

- [создать основную команду Секции](create-partition-primary.md)

- [Команда удаления секции](delete-partition.md)

- [Команда "подробное секционирование"](detail-partition.md)

- [Команда "выбрать диск"](select-disk.md)

- [команда SELECT VDISK](select-vdisk.md)

- [Команда "выбрать том"](select-volume.md)
