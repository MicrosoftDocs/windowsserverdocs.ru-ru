---
title: convert basic
description: Справочная статья по команде Convert Basic, которая преобразует пустой динамический диск в базовый.
ms.topic: reference
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 40272dc22d526bac90a59776f3cc3d1023d29d7b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819598"
---
# <a name="convert-basic"></a>convert basic

Преобразует пустой динамический диск в базовый. Для выполнения этой операции должен быть выбран динамический диск. Используйте [команду Выбор диска](select-disk.md) , чтобы выбрать динамический диск и переместить фокус на него.

> [!IMPORTANT]
> Диск должен быть пустым, чтобы преобразовать его в базовый диск. Создайте резервную копию данных, а затем удалите все разделы или тома перед преобразованием диска.

> [!NOTE]
> Инструкции по использованию этой команды см. в разделе [Переключение динамического диска обратно на базовый диск](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc755238(v=ws.11)).

## <a name="syntax"></a>Синтаксис

```
convert basic [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="examples"></a>Примеры

Чтобы преобразовать выбранный динамический диск в базовый, введите:

```
convert basic
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [преобразовать команду](convert.md)
