---
title: regsvr32
description: Справочная статья по команде regsvr32, которая регистрирует DLL-файлы как компоненты команды в реестре.
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a591813480163a6d43329222d20e2a29651f576
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883887"
---
# <a name="regsvr32"></a>regsvr32

Регистрирует DLL-файлы в качестве компонентов команды в реестре.

## <a name="syntax"></a>Синтаксис

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <Dllname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание: |
|--|--|
| /U | Отменяет регистрацию сервера. |
| /s | Предотвращает отображение сообщений. |
| /n | Предотвращает вызов функции **DllRegisterServer**. Этот параметр требует также использования параметра **/i** . |
| /i`<cmdline>` | Передает необязательную строку командной строки (*cmdline*) в **DllInstall**. При использовании этого параметра с параметром **/u** вызывается **дллунинсталл**. |
| `<Dllname>` | Имя DLL-файла, который будет зарегистрирован. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы зарегистрировать библиотеку. dll для схемы Active Directory, введите:

```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
