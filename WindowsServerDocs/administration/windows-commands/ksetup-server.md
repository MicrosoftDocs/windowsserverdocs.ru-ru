---
title: ksetup server
description: Справочная статья по команде сервера ksetup, которая позволяет указать имя компьютера под управлением операционной системы Windows, поэтому изменения, внесенные командой ksetup, обновляют конечный компьютер.
ms.topic: reference
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bab6306cd933840416c263e7a94122a87a3705dd
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814858"
---
# <a name="ksetup-server"></a>ksetup server

Позволяет указать имя компьютера под управлением операционной системы Windows, поэтому изменения, внесенные командой **ksetup** , обновляют целевой компьютер.

Имя целевого сервера хранится в реестре в разделе `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos` . Эта запись не отображается при выполнении команды **ksetup** .

> [!IMPORTANT]
> Удалить имя целевого сервера невозможно. Вместо этого можно вернуться к локальному имени компьютера, используемому по умолчанию.

## <a name="syntax"></a>Синтаксис

```
ksetup /server <servername>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<servername>` | Указывает полное имя компьютера, на котором будет действовать конфигурация, например *IPops897.Corp.contoso.com*.<p>Если указано неполное полное доменное имя компьютера, команда завершится ошибкой. |

### <a name="examples"></a>Примеры

Чтобы обеспечить эффективную настройку **ksetup** на компьютере *IPops897* , подключенном к домену contoso, введите:

```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)
