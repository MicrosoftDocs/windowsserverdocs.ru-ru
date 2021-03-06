---
title: logman create alert
description: Справочная статья по команде Logman Create Alert, которая создает сборщик данных предупреждений.
ms.topic: reference
ms.assetid: 93e6fc2b-5bf5-413b-84b4-be8b9dd3a57d
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4c914ad82ea03bd5a66bef5c019d32e4024a039e
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101814100"
---
# <a name="logman-create-alert"></a>logman create alert

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает сборщик данных предупреждений.

## <a name="syntax"></a>Синтаксис

```
logman create alert <[-n] <name>> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -s `<computer name>` | Выполните команду на указанном удаленном компьютере. |
| -config `<value>` | Указывает файл параметров, содержащий параметры команды. |
| [-n] `<name>` | Имя целевого объекта. |
| -[-] u `<user [password]>` | Указывает пользователя для запуска от имени. При вводе `*` для пароля выводится запрос на ввод пароля. Пароль не отображается при вводе. |
| -m `<[start] [stop] [[start] [stop] [...]]>` | Изменения в начале или в ручном режиме вместо запланированного начала или окончания. |
| -RF `<[[hh:]mm:]ss>` | Запускает сборщик данных за указанный период времени. |
| -б `<M/d/yyyy h:mm:ss[AM|PM]>` | Начинает сбор данных в указанное время. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | Завершает сбор данных в указанное время. |
| -Si `<[[hh:]mm:]ss>` | Указывает интервал выборки для собираются данных счетчиков производительности. |
| -o `<path|dsn!log>` | Указывает выходной файл журнала или имя DSN и набора журналов в базе данных SQL. |
| -[-] r | Повторяет сборщик данных ежедневно с заданным временем начала и окончания. |
| -[-] a | Добавляет существующий файл журнала. |
| -[-] | Перезаписывает существующий файл журнала. |
| -[-] v `<nnnnnn|mmddhhmm>` | Присоединяет сведения о управлении версиями файлов к концу имени файла журнала. |
| -[-] RC `<task>` | Выполняет команду, указанную при каждом закрытии журнала. |
| -[-] максимум `<value>` | Максимальный размер файла журнала (в МБ или в максимальном количестве записей для журналов SQL). |
| -[-] cnf `<[[hh:]mm:]ss>` | Если указано время, создает новый файл по истечении указанного времени. Если параметр time не указан, создает новый файл при превышении максимального размера. |
| -y | Отвечает Да на все вопросы без запроса. |
| -CF `<filename>` | Указывает файл со списком счетчиков производительности для накопления. Файл должен содержать по одному имени счетчика производительности в строке. |
| -[-] El | Включает или отключает отчеты журнала событий. |
| -й `<threshold [threshold [...]]>` | Укажите счетчики и их пороговые значения для предупреждения. |
| -[-] RDC `<name>` | Указывает группу сборщиков данных, запускаемую при срабатывании предупреждения. |
| -[-] тн `<task>` | Указывает задачу, выполняемую при срабатывании оповещения. |
| -[-] коне `<argument>` | Указывает аргументы задачи, которые будут использоваться с задачей, заданной с помощью-тн. |
| /? | Отображает контекстную справку. |

#### <a name="remarks"></a>Комментарии

- Где [-] присутствует, Добавление дополнительного дефиса (-) инвертирует параметр.

### <a name="examples"></a>Примеры

Чтобы создать новое предупреждение с именем, *new_alert*, которое срабатывает, когда счетчик производительности "% загруженности процессора" в группе счетчиков "процессор (_Total)" превышает значение счетчика 50, введите:

```
logman create alert new_alert -th \Processor(_Total)\% Processor time>50
```

> [!NOTE]
> Заданное пороговое значение основано на значении, собираемом счетчиком, поэтому в этом примере значение 50 равно 50% времени процессора.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда logman Update Alert](logman-update-alert.md)

- [команда logman](logman.md)
