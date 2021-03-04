---
title: scwcmd
description: Справочная статья по средству командной строки scwcmd.exe, входящему в состав мастера настройки безопасности (SCW).
ms.topic: reference
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f968ffb1f840404768564b337467ecfff78d4a47
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806267"
---
# <a name="scwcmd"></a>scwcmd

> Область применения: Windows Server 2012 R2 и Windows Server 2012

Программу командной строки Scwcmd.exe, входящую в состав мастера настройки безопасности (SCW), можно использовать для выполнения следующих задач.

- Проанализируйте один или несколько серверов с помощью политики, созданной SCW.

- Настройте один или несколько серверов с помощью политики, созданной SCW.

- Зарегистрируйте расширение базы данных конфигурации безопасности с помощью SCW.

- Откат политик SCW.

- Преобразование созданной SCW политики в собственные файлы, которые поддерживаются групповая политика.

- Просмотр результатов анализа в формате HTML.

> [!NOTE]
> Если для настройки, анализа или отката политики на удаленном сервере используется **команду scwcmd** , SCW должен быть установлен на удаленном сервере.

## <a name="syntax"></a>Синтаксис

```
scwcmd analyze
scwcmd configure
scwcmd register
scwcmd rollback
scwcmd transform
scwcmd view
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| [scwcmd analyze](scwcmd-analyze.md) | Определяет, соответствует ли компьютер политике. |
| [scwcmd configure](scwcmd-configure.md) | Применяет политику безопасности, созданную SCW, к компьютеру.|
| [scwcmd register](scwcmd-register.md) | Расширяет или настраивает базу данных конфигурации безопасности SCW путем регистрации файла базы данных конфигурации безопасности, содержащего определения ролей, задач, служб или портов. |
| [scwcmd rollback](scwcmd-rollback.md) | Применяет последнюю доступную политику отката, а затем удаляет эту политику отката. |
| [scwcmd transform](scwcmd-transform.md) | Преобразует файл политики безопасности, созданный с помощью SCW, в новый объект групповая политика (GPO) в службах домен Active Directory Services. |
| [scwcmd view](scwcmd-view.md) | Визуализирует XML-файл с помощью указанного преобразования XSL. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
