---
title: scwcmd transform
description: Справочная статья по команде преобразования команду scwcmd, которая преобразует файл политики безопасности, созданный с помощью мастера настройки безопасности (SCW), в новый объект групповая политика (GPO) в службах домен Active Directory Services.
ms.topic: reference
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d6588f14a83d446a129825c0b7fa07fb109bd517
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806347"
---
# <a name="scwcmd-transform"></a>scwcmd transform

> Область применения: Windows Server 2012 R2 и Windows Server 2012

Преобразует файл политики безопасности, созданный с помощью мастера настройки безопасности (SCW), в новый объект групповая политика (GPO) в службах домен Active Directory Services. Операция преобразования не изменяет никаких параметров на сервере, на котором он выполняется. После завершения операции преобразования администратор должен связать объект GPO с нужными подразделениями, чтобы развернуть политику на серверах.

> [!IMPORTANT]
> Для завершения операции преобразования требуются учетные данные администратора домена.
>
> Не удается развернуть параметры политики безопасности службы IIS (IIS) с помощью групповая политика.
>
> Политики брандмауэра, в которых перечисляются утвержденные приложения, не должны развертываться на серверах, если служба брандмауэра Windows не была автоматически запущена при последнем запуске сервера.

## <a name="syntax"></a>Синтаксис

```
scwcmd transform /p:<policyfile.xml> /g:<GPOdisplayname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /p`<policyfile.xml>` | Указывает путь и имя файла политики XML, который следует применить. Этот параметр должен быть указан. |
| /g`<GPOdisplayname>` | Указывает отображаемое имя объекта групповой политики. Этот параметр должен быть указан. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы создать объект групповой политики с именем *филесерверсекурити* из файла с именем *FileServerPolicy.xml*, введите:

```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда команду scwcmd Analyze](scwcmd-analyze.md)

- [команду scwcmd configure, команда](scwcmd-configure.md)

- [команду scwcmd Register, команда](scwcmd-register.md)

- [команда отката команду scwcmd](scwcmd-rollback.md)

- [Команда команду scwcmd view](scwcmd-view.md)