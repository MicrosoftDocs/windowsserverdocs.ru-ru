---
title: uniqueid
description: Справочная статья по UniqueId, которая отображает или задает идентификатор таблицы разделов GUID (GPT) или подпись основной загрузочной записи (MBR) для диска с фокусом.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5acf29d9a7dfd505a5ecdad2a08dfdb1a9f4d975
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937283"
---
# <a name="uniqueid"></a>uniqueid

Отображает или задает идентификатор таблицы разделов GUID (GPT) или подпись основной загрузочной записи (MBR) для диска, на котором находится фокус.

> [!IMPORTANT]
> Эта команда DiskPart недоступна ни в одном из выпусков Windows Vista.

## <a name="syntax"></a>Синтаксис

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

### <a name="parameters"></a>Параметры

|  Параметр   |                                                                                             Описание                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ИД = {\<dword> |                                                                                               <GUID>}                                                                                                |
|    Noerr     | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="remarks"></a>Комментарии

-   Эта команда работает на базовых и динамических дисках.
-   Для завершения этой команды необходимо выбрать диск. Используйте команду **Выбор диска** , чтобы выбрать диск и переместить фокус на него.

## <a name="examples"></a>Примеры

Чтобы отобразить подпись диска MBR с фокусом, введите:
```
uniqueid disk
```
Чтобы задать подпись диска MBR с фокусом на 5f1b2c36, введите:
```
uniqueid disk id=5f1b2c36
```
Чтобы задать идентификатор диска GPT с фокусом на baf784e7-6bbd-4cfb-aaac-e86c96e166ee, введите:
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

## <a name="additional-references"></a>Дополнительные ссылки

