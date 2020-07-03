---
title: attributes volume
description: Справочная статья по команде атрибуты тома, которая отображает, устанавливает или удаляет атрибуты тома.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aae7cc7fe26fac5ef03e40610eb46389eb274c94
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923870"
---
# <a name="attributes-volume"></a>attributes volume

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает, устанавливает или очищает атрибуты тома.

## <a name="syntax"></a>Синтаксис

```
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ------- | -------- |
| set | Задает указанный атрибут тома с фокусом. |
| clear | Очищает указанный атрибут тома с фокусом. |
| readonly | Указывает, что том доступен только для чтения. |
| hidden | Указывает, что том скрыт. |
| нодефаултдривелеттер | Указывает, что том не получает букву диска по умолчанию. |
| SHADOWCOPY | Указывает, что том является томом теневого копирования. |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

### <a name="remarks"></a>Комментарии

- На основных дисках основной загрузочной записи (MBR) параметры **Hidden**, **ReadOnly**и **нодефаултдривелеттер** применяются ко всем томам на диске.

- На основных дисках таблицы разделов GPT, а также на динамических дисках MBR и GPT параметры **Hidden**, **ReadOnly**и **нодефаултдривелеттер** применяются только к выбранному тому.

- Чтобы команда **атрибутов тома** была выполнена, необходимо выбрать том. Используйте команду **выбрать том** , чтобы выбрать том и переместить фокус на него.

## <a name="examples"></a>Примеры

Чтобы отобразить текущие атрибуты выбранного тома, введите:

```
attributes volume
```

Чтобы задать выбранный том как скрытый и только для чтения, введите:

```
attributes volume set hidden readonly
```

Чтобы удалить скрытые и атрибуты только для чтения на выбранном томе, введите:

```
attributes volume clear hidden readonly
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда "выбрать том"](select-volume.md)
