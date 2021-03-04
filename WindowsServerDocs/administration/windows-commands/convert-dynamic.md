---
title: convert dynamic
description: Справочная статья по динамической команде Convert, преобразующая базовый диск в динамический диск.
ms.topic: reference
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4aa2f12b42db2efd522f4eeebfb824e6855d5273
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819588"
---
# <a name="convert-dynamic"></a>convert dynamic

Преобразует базовый диск в динамический диск. Для выполнения этой операции необходимо выбрать базовый диск. Используйте [команду Выбор диска](select-disk.md) , чтобы выбрать базовый диск и переместить фокус на него.

> [!NOTE]
> Инструкции по использованию этой команды см. в разделе [Переключение динамического диска обратно на базовый диск](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc755238(v=ws.11)).

## <a name="syntax"></a>Синтаксис

```
convert dynamic [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

#### <a name="remarks"></a>Комментарии

- Все существующие разделы на базовом диске становятся простыми томами.

## <a name="examples"></a>Примеры

Чтобы преобразовать базовый диск в динамический, введите:

```
convert dynamic
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [преобразовать команду](convert.md)
