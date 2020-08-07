---
title: Vssadmin удаление теней
description: Описание команды vssadmin Delete Shadows.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 884407cee82926b3b258afba5ab2e47dc640e10f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891810"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin удаление теней

> Область применения: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Удаляет теневые копии указанного тома.

## <a name="syntax"></a>Синтаксис

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание:|
|---|---|
|/фор =\<ForVolumeSpec>|Указывает, какой из теневых копий тома будет удален.|
|/олдест|Удаляет только самую старую теневую копию.|
|/all|Удаляет все заданные теневые копии тома.|
|/Шадов =\<ShadowID>|Удаляет теневую копию, указанную параметром Шадовид. Чтобы получить идентификатор теневой копии, используйте команду **vssadmin List Shadows** . При вводе идентификатора теневой копии используйте следующий формат, где каждый *X* представляет шестнадцатеричный символ:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/quiet|Указывает, что команда не будет отображать сообщения во время выполнения.|

## <a name="remarks"></a>Remarks

Удалять можно только теневые копии с типом, доступным для клиента.

## <a name="examples"></a>Примеры

Чтобы удалить самую старую теневую копию тома C, введите следующую команду:

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Дополнительные ссылки

* [Ключ синтаксиса командной строки](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [List](vssadmin.md)
* [Vssadmin List Shadows](vssadmin-list-shadows.md)
