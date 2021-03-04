---
title: uniqueid
description: Справочная статья по UniqueId, которая отображает или задает идентификатор таблицы разделов GUID (GPT) или подпись основной загрузочной записи (MBR) для диска с фокусом.
ms.topic: reference
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b38a76b41fc2732b16d296d4e8fd4eca6f885d62
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804757"
---
# <a name="uniqueid"></a>uniqueid

Отображает или задает идентификатор таблицы разделов GUID (GPT) или подпись основной загрузочной записи (MBR) для базового или динамического диска с фокусом. Для выполнения этой операции необходимо выбрать базовый или динамический диск. Используйте [команду Выбор диска](select-disk.md) , чтобы выбрать диск и переместить фокус на него.

## <a name="syntax"></a>Синтаксис

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| Идентификатор =`{<dword> | <GUID>}` | Для MBR-дисков этот параметр задает 4-байтовый (DWORD) параметр в шестнадцатеричной форме для подписи. Для дисков GPT этот параметр указывает идентификатор GUID для идентификатора. |
| Noerr | Только для сценариев. При возникновении ошибки программа DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="examples"></a>Примеры

Чтобы отобразить подпись диска MBR с фокусом, введите:

```
uniqueid disk
```

Чтобы задать в качестве подписи диска MBR значение DWORD *5f1b2c36*, введите:

```
uniqueid disk id=5f1b2c36
```

Чтобы задать идентификатор диска GPT с фокусом на значение GUID baf784e7-6bbd-4cfb-aaac-e86c96e166ee, введите:

```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда "выбрать диск"](select-disk.md)
