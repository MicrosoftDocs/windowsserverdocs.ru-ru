---
title: scwcmd
description: Справочная статья по средству командной строки scwcmd.exe, входящему в состав мастера настройки безопасности (SCW).
ms.topic: reference
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 87bd2c718bec18810026c5701b955d5ef655b53e
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388924"
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
