---
title: regsvr32
description: Справочный раздел по * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: beadc9e9e614e2fe4cffad5dc263cfb1d4aecf67
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722477"
---
# <a name="regsvr32"></a>regsvr32



Регистрирует DLL-файлы в качестве компонентов команды в реестре.



## <a name="syntax"></a>Синтаксис

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|/U|Отменяет регистрацию сервера.|
|/s|Запускает **regsvr32** без отображения сообщений.|
|/n|Запускает **regsvr32** без вызова функции **DllRegisterServer**. (Требуется параметр **/i** .)|
|/i:\<cmdline>|Передает необязательную строку командной строки (*cmdline*) в **DllInstall**. Если этот параметр используется вместе с параметром **/u** , он вызывает **дллунинсталл**.|
|\<DllName>|Имя DLL-файла, который будет зарегистрирован.|
|/?|Отображение справки в командной строке.|

## <a name="examples"></a>Примеры

Чтобы зарегистрировать библиотеку. dll для схемы Active Directory, введите:
```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)