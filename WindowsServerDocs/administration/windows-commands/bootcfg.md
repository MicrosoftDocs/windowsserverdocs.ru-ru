---
title: bootcfg
description: Справочная статья по команде bootcfg, которая настраивает, запрашивает или изменяет Boot.ini параметры файлов.
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: edab8bc0b4e63544282e53f0a7b6e1fc255a4be7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880520"
---
# <a name="bootcfg"></a>bootcfg

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Настраивает, запрашивает или изменяет Boot.ini параметров файлов.

## <a name="syntax"></a>Синтаксис

```
bootcfg <parameter> [arguments...]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
| --------- | ----------- |
| [bootcfg addsw](bootcfg-addsw.md) | Добавляет параметры загрузки операционной системы для указанной записи операционной системы. |
| [bootcfg copy](bootcfg-copy.md) | Создает копию существующей записи загрузки, в которую можно добавить параметры командной строки. |
| [bootcfg dbg1394](bootcfg-dbg1394.md) | Настраивает отладку порта 1394 для указанной записи операционной системы. |
| [bootcfg debug](bootcfg-debug.md) | Добавляет или изменяет параметры отладки для указанной записи операционной системы. |
| [bootcfg default](bootcfg-default.md) | Указывает запись операционной системы, которую следует назначить по умолчанию. |
| [bootcfg delete](bootcfg-delete.md) | Удаляет запись операционной системы в разделе [Operating Systems] файла Boot.ini. |
| [bootcfg ems](bootcfg-ems.md) | Позволяет пользователю добавлять или изменять параметры перенаправления консоли служб аварийного управления на удаленный компьютер. |
| [bootcfg query](bootcfg-query.md) | Запрашивает и отображает записи разделов [boot loader] и [Operating Systems] из Boot.ini. |
| [bootcfg raw](bootcfg-raw.md) | Добавляет параметры загрузки операционной системы, указанные в виде строки, в запись операционной системы в разделе [Operating Systems] файла Boot.ini. |
| [bootcfg rmsw](bootcfg-rmsw.md) | Удаляет параметры загрузки операционной системы для указанной записи операционной системы. |
| [bootcfg timeout](bootcfg-timeout.md) | Изменяет значение времени ожидания операционной системы. |
