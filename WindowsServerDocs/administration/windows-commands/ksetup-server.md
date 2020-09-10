---
title: ksetup server
description: Справочная статья по команде сервера ksetup, которая позволяет указать имя компьютера под управлением операционной системы Windows, поэтому изменения, внесенные командой ksetup, обновляют конечный компьютер.
ms.topic: reference
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4be82315bc0d683b5399350c618aa87e615067ba
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639575"
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
