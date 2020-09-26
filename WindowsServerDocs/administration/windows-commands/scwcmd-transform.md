---
title: scwcmd transform
description: Справочная статья по команде преобразования команду scwcmd, которая преобразует файл политики безопасности, созданный с помощью мастера настройки безопасности (SCW), в новый объект групповая политика (GPO) в службах домен Active Directory Services.
ms.topic: reference
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bef3d9800d19ac0e3e574b4ef2e1195dcdc3baed
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389257"
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