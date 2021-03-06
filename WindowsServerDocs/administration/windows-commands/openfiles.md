---
title: openfiles
description: Справочная статья по команде openfiles, которая позволяет администратору запрашивать, отображать или отключать файлы и каталоги, открытые в системе.
ms.topic: reference
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 65f835a71167e81d4ef0b7cd6266c7edf625542f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101808979"
---
# <a name="openfiles"></a>openfiles

Позволяет администратору запрашивать, отображать или отключать файлы и каталоги, открытые в системе. Эта команда также включает или отключает глобальный флаг System **обслуживание списка объектов** .

## <a name="openfiles-disconnect"></a>Openfiles/Disconnect

Позволяет администратору отключить файлы и папки, открытые удаленно через общую папку.

### <a name="syntax"></a>Синтаксис

```
openfiles /disconnect [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] {[/id <openfileID>] | [/a <accessedby>] | [/o {read | write | read/write}]} [/op <openfile>]
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| ключ `<system>` | Указывает удаленную систему для подключения (по имени или IP-адресу). Не используйте обратные косые черты. Если параметр **/s** не используется, команда по умолчанию выполняется на локальном компьютере. Этот параметр применяется ко всем файлам и папкам, указанным в команде. |
| /u `[<domain>\]<username>` | Выполняет команду, используя разрешения указанной учетной записи пользователя. Если параметр **/u** не используется, по умолчанию используются разрешения системы. |
| /p `[<password>]` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . Если вы не используете параметр **/p** , при выполнении команды появится запрос на ввод пароля. |
| /ID `<openfileID>` | Отключает открытые файлы по указанному ИДЕНТИФИКАТОРу файла. С этим параметром можно использовать подстановочный знак (**&#42;**).<p>Примечание. для поиска идентификатора файла можно использовать команду **openfiles/Query** . |
| / `<accessedby>` | Отключает все открытые файлы, связанные с именем пользователя, указанным в параметре *акцесседби* . С этим параметром можно использовать подстановочный знак (**&#42;**). |
| /o `{read | write | read/write}` | Отключает все открытые файлы с указанным значением в открытом режиме. Допустимые значения: **Чтение**, **запись**, **чтение и запись**. С этим параметром можно использовать подстановочный знак (**&#42;**). |
| /Op `<openfile>` | Отключает все соединения открытых файлов, созданные с помощью определенного имени открытого файла. С этим параметром можно использовать подстановочный знак (**&#42;**). |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы отключить все открытые файлы с помощью *идентификатора файла 26843578*, введите:

```
openfiles /disconnect /id 26843578
```

Чтобы отключить все открытые файлы и каталоги, к которым обращается пользователь *хироплн*, введите:

```
openfiles /disconnect /a hiropln
```

Чтобы отключить все открытые файлы и каталоги с *режимом чтения и записи*, введите:

```
openfiles /disconnect /o read/write
```

Чтобы отключить каталог с открытым именем файла * К:\тестшаре \* , независимо от того, кто обращается к нему, введите:

```
openfiles /disconnect /a * /op c:\testshare\
```

Чтобы отключить все открытые файлы на удаленном компьютере *срвмаин* , к которым обращается пользовательская *хироплн*, независимо от их идентификатора, введите:

```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="openfiles-query"></a>Openfiles/Query

Запрашивает и отображает все открытые файлы.

### <a name="syntax"></a>Синтаксис

```
openfiles /query [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

#### <a name="parameters"></a>Параметры


| Параметр | Описание |
|--|--|
| ключ `<system>` | Указывает удаленную систему для подключения (по имени или IP-адресу). Не используйте обратные косые черты. Если параметр **/s** не используется, команда по умолчанию выполняется на локальном компьютере. Этот параметр применяется ко всем файлам и папкам, указанным в команде. |
| /u `[<domain>\]<username>` | Выполняет команду, используя разрешения указанной учетной записи пользователя. Если параметр **/u** не используется, по умолчанию используются разрешения системы. |
| /p `[<password>]` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . Если вы не используете параметр **/p** , при выполнении команды появится запрос на ввод пароля. |
| [/FO `{TABLE | LIST | CSV}` ] | Отображает выходные данные в указанном формате. Допустимые значения:<ul><li>**Таблица** — отображает выходные данные в таблице.</li><li>**List** — отображает выходные данные в списке.</li><li>**CSV** — отображает выходные данные в формате с разделителями-запятыми (CSV).</li></ul> |
| использован | Подавляет вывод заголовков столбцов в выходных данных. Допустим, только если параметр **/FO** имеет значение **Table** или **CSV**. |
| /v | Указывает, что в выходных данных отображаются подробные (подробные) сведения. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы запросить и отобразить все открытые файлы, введите:

```
openfiles /query
```

Чтобы запросить и отобразить все открытые файлы в формате таблицы без заголовков, введите:

```
openfiles /query /fo table /nh
```

Чтобы запросить и отобразить все открытые файлы в формате списка с подробными сведениями, введите:

```
openfiles /query /fo list /v
```

Чтобы запросить и отобразить все открытые файлы в удаленной системе *срвмаин* , используя учетные данные пользователя *хироплн* в домене *маиндом* , введите:

```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> В этом примере пароль указан в командной строке. Чтобы запретить отображение пароля, оставьте параметр **/p** . Вам будет предложено ввести пароль, который не будет отображаться на экране.

## <a name="openfiles-local"></a>Openfiles/Local

Включает или отключает глобальный флаг System **обслуживании списка объектов** . Если используется без параметров, то **openfiles/Local** отображает текущее состояние флага " **сохранить глобальный список объектов** ".

> [!NOTE]
> Изменения, внесенные с помощью параметра **вкл** . или **выкл** ., вступают в силу только после перезагрузки системы. Включение глобального флага " **Ведение списка объектов** " может замедлить работу системы.

### <a name="syntax"></a>Синтаксис

```
openfiles /local [on | off]
```

#### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `[on | off]` | Включает или отключает глобальный флаг System **обслуживание списка объектов** , который отслеживает дескрипторы локальных файлов. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

Чтобы проверить текущее состояние глобального флага " **сохранить список объектов** ", введите:

```
openfiles /local
```

По умолчанию глобальный флаг « **Ведение списка объектов** » отключен, и появляется следующее сообщение: `INFO: The system global flag 'maintain objects list' is currently disabled.`

Чтобы включить глобальный флаг " **Ведение списка объектов** ", введите:

```
openfiles /local on
```

При включении глобального флага появляется следующее сообщение: `SUCCESS: The system global flag 'maintain objects list' is enabled. This will take effect after the system is restarted.`

Чтобы отключить глобальный флаг " **Ведение списка объектов** ", введите:

```
openfiles /local off
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
