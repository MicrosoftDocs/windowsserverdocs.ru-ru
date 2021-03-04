---
title: clean
description: Справочная статья по команде DiskPart Clean, которая удаляет все разделы или форматирование тома с диска, на котором находится фокус.
ms.topic: reference
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6855000c695d98016ee99d28ca68f3080ad0f2b4
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819837"
---
# <a name="clean"></a>clean

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет все разделы или форматирование тома с диска, на котором находится фокус.

>[!NOTE]
> Версию этой команды для PowerShell см. в разделе [Команда Clear-Disk](/powershell/module/storage/clear-disk).

## <a name="syntax"></a>Синтаксис

```
clean [all]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| все | Указывает, что каждый сектор диска имеет значение 0, что полностью удаляет все данные, содержащиеся на диске. |

#### <a name="remarks"></a>Комментарии

- На дисках основной загрузочной записи (MBR) перезаписываются только сведения о разделах MBR и скрытых секторах.

- На дисках с таблицей разделов GPT сведения о секционировании GPT, включая защитный код MBR, перезаписываются. Нет сведений о скрытых секторах.

- Для выполнения этой операции необходимо выбрать диск. Используйте команду **Выбор диска** , чтобы выбрать диск и переместить фокус на него.

## <a name="examples"></a>Примеры

Чтобы удалить все форматирование с выбранного диска, введите:

```
clean
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Команда Clear-Disk](/powershell/module/storage/clear-disk)

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
