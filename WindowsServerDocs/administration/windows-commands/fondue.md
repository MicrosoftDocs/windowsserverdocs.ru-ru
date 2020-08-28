---
title: фондю
description: Справочная статья по команде фондуе, которая включает дополнительные компоненты Windows, загружая необходимые файлы из Центр обновления Windows или другого источника, указанного групповая политика.
ms.topic: reference
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 132441d48ce1f65b38955130fe19535775d02377
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035072"
---
# <a name="fondue"></a>фондю

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Включает дополнительные компоненты Windows, загружая необходимые файлы из Центр обновления Windows или другого источника, указанного групповая политика. Файл манифеста для компонента уже должен быть установлен в образе Windows.

## <a name="syntax"></a>Синтаксис

```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootrequest}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /Enable-Feature`<feature_name>` | Указывает имя необязательного компонента Windows, который требуется включить. В командную строку можно включить только один компонент. Чтобы включить несколько функций, используйте fondue.exe для каждого компонента. |
| /Каллер-наме:`<program_name>` | Указывает имя программы или процесса при вызове fondue.exe из скрипта или пакетного файла. Этот параметр можно использовать для добавления имени программы в отчет SQM при возникновении ошибки. |
| /Хиде-УКС:`{all | rebootrequest}` | Используйте **ALL** , чтобы скрыть все сообщения для пользователя, включая ход выполнения и запросы разрешений на доступ к центр обновления Windows. Если требуется разрешение, операция завершится ошибкой.<p>Используйте **ребутрекуест** , чтобы скрыть только пользовательские сообщения, запрашивающие разрешение на перезагрузку компьютера. Используйте этот параметр, если у вас есть сценарий, управляющий запросами на перезагрузку. |

### <a name="examples"></a>Примеры

Чтобы включить Microsoft .NET Framework 4,8, введите:

```
fondue.exe /enable-feature:NETFX4
```

Чтобы включить Microsoft .NET Framework 4,8, добавьте имя программы в отчет SQM и не выводите сообщения пользователю, введите:

```
fondue.exe /enable-feature:NETFX4 /caller-name:Admin.bat /hide-ux:all
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Загрузка Microsoft .NET Framework 4,8](https://dotnet.microsoft.com/download/dotnet-framework/net48)
