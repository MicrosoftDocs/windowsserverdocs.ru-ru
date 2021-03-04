---
title: detach vdisk
description: Справочная статья по команде Detach vdisk, которая останавливает выбранный виртуальный жесткий диск (VHD) в качестве локального жесткого диска на главном компьютере.
ms.topic: reference
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b3383cffbc7c0ea58945ff26fb634614843877b0
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101819038"
---
# <a name="detach-vdisk"></a>detach vdisk

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Останавливает отображение выбранного виртуального жесткого диска (VHD) в качестве локального жесткого диска на главном компьютере. При отсоединении виртуального жесткого диска его можно скопировать в другие расположения. Прежде чем начать, необходимо выбрать виртуальный жесткий диск для выполнения этой операции. Используйте команду [SELECT VDISK](select-vdisk.md) , чтобы выбрать виртуальный жесткий диск и переместить фокус на него.


## <a name="syntax"></a>Синтаксис

```
detach vdisk [noerr]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| Noerr | Только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="examples"></a>Примеры

Чтобы отсоединить выбранный виртуальный жесткий диск, введите:

```
detach vdisk
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Attach vdisk](attach-vdisk.md)

- [Команда Compact VDISK](compact-vdisk.md)

- [Команда Detail VDISK](detail-vdisk.md)

- [Команда Expand VDISK](expand-vdisk.md)

- [Команда merge VDISK](merge-vdisk.md)

- [команда SELECT VDISK](select-vdisk.md)

- [Команда list](list.md)
