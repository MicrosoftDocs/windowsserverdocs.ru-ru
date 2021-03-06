---
title: auditpol set
description: Справочная статья по команде auditpol Set, которая задает политику аудита для отдельных пользователей, политику аудита системы или параметры аудита.
ms.topic: reference
ms.assetid: f4947486-87bd-48cb-ba81-7230c8e70895
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 293460b98db974b63bad473a48dfcd4f941a8256
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101823098"
---
# <a name="auditpol-set"></a>auditpol set

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Задает политику аудита "на пользователя", политику аудита системы или параметры аудита.

Для выполнения операций *Set* с политиками на *уровне пользователя* и *системы* необходимо иметь разрешение на **запись** или **полный** доступ для этого набора объектов в дескрипторе безопасности. Вы также можете выполнять операции *Set* , если у вас есть права пользователя " **Управление аудитом и журналом безопасности** " (SeSecurityPrivilege). Однако это право предоставляет дополнительный доступ, ненеобходимый для выполнения общих операций *Set* .

## <a name="syntax"></a>Синтаксис

```
auditpol /set
[/user[:<username>|<{sid}>][/include][/exclude]]
[/category:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/subcategory:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/option:<option name> /value: <enable>|<disable>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| WMIC | Субъект безопасности, для которого задана политика аудита "на пользователя", заданная категорией или подкатегорией. Необходимо указать либо параметр Category, либо Подкатегория, в качестве идентификатора безопасности (SID) или имени. |
| /include | Указывается с параметром/User; Указывает, что политика для пользователя будет создавать аудит, даже если он не задан политикой аудита системы. Этот параметр используется по умолчанию и применяется автоматически, если не указаны явно параметры/include и/Exclude. |
| /Exclude | Указывается с параметром/User; Указывает, что политика пользователя заблокирует аудит вне зависимости от политики аудита системы. Этот параметр не учитывается для пользователей, являющихся членами локальной группы "Администраторы". |
| /category | Одна или несколько категорий аудита, заданные глобальным уникальным идентификатором (GUID) или именем. Если пользователь не указан, задается системная политика. |
| /субкатегори | Одна или несколько подкатегорий аудита, заданные с помощью GUID или имени. Если пользователь не указан, задается системная политика. |
| /сукцесс | Указывает аудит успехов. Этот параметр используется по умолчанию и применяется автоматически, если не указаны явно параметры/сукцесс и/фаилуре. Этот параметр должен использоваться с параметром, указывающим, следует ли включать или отключать параметр. |
| /фаилуре | Указывает аудит сбоев. Этот параметр должен использоваться с параметром, указывающим, следует ли включать или отключать параметр. |
| /параметр | Задает политику аудита для параметров CrashOnAuditFail, Фуллпривилежеаудитинг, Аудитбасеобжектс или Аудитбаседиректориес. |
| /SD | Задает дескриптор безопасности, используемый для делегирования доступа к политике аудита. Дескриптор безопасности должен быть указан с помощью языка определения дескрипторов безопасности (SDDL). Дескриптор безопасности должен иметь список управления доступом на уровне пользователей (DACL). |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы задать политику аудита для каждого пользователя для всех подкатегорий в подробной категории отслеживания для пользователя микедан таким образом, чтобы все успешные попытки пользователя были проверены, введите:

```
auditpol /set /user:mikedan /category:detailed Tracking /include /success:enable
```

Чтобы задать политику аудита для каждого пользователя для категорий, заданных по имени и идентификатору GUID, а также подкатегории, заданные идентификатором GUID, чтобы отключить аудит для любых успешных или неудачных попыток, введите:

```
auditpol /set /user:mikedan /exclude /category:Object Access,System,{6997984b-797a-11d9-bed3-505054503030}
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```

Чтобы задать политику аудита "на пользователя" для указанного пользователя для всех категорий, чтобы подавить аудит всех, но успешных попыток, введите:
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```

Чтобы установить политику аудита системы для всех подкатегорий в подробной категории отслеживания, чтобы включить аудит только успешных попыток, введите:

```
auditpol /set /category:detailed Tracking /success:enable
```

> [!NOTE]
> Параметр сбоя не изменяется.

Чтобы задать политику аудита системы для доступа к объектам и категорий системы (что подразумевается, так как перечислены подкатегории) и подкатегории, заданные идентификаторами GUID для подавления неудачных попыток и аудита успешных попыток, введите:

```
auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
```

Чтобы установить параметры аудита в состояние "включено" для параметра CrashOnAuditFail, введите:

```
auditpol /set /option:CrashOnAuditFail /value:enable
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команды auditpol](auditpol.md)
