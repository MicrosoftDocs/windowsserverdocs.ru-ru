---
title: reg query
description: Справочная статья по команде reg query, которая возвращает список следующего уровня подразделов и записей, расположенных в указанном подразделе реестра.
ms.topic: reference
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9a83309d7a6b21cc668622ceb2e50de72b4fc63f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101807197"
---
# <a name="reg-query"></a>reg query

Возвращает список следующего уровня подразделов и записей, расположенных в указанном подразделе реестра.

## <a name="syntax"></a>Синтаксис

```
reg query <keyname> [{/v <Valuename> | /ve}] [/s] [/se <separator>] [/f <data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<keyname>` | Указывает полный путь к подразделу. Чтобы указать удаленный компьютер, включите имя компьютера (в формате `\\<computername>\` ) в состав имени *keyName*. Пропуск `\\<computername>\` приводит к тому, что по умолчанию операция выполняется на локальном компьютере. *KeyName* должен содержать допустимый корневой ключ. Допустимые корневые ключи для локального компьютера: **HKLM**, **HKCU**, **HKCR**, **HKU** и **хккк**. Если указан удаленный компьютер, допустимые корневые ключи: **HKLM** и **HKU**. Если имя раздела реестра содержит пробел, заключите имя ключа в кавычки. |
| /v `<Valuename>` | Указывает имя значения реестра для запроса. Если этот параметр опущен, возвращаются все имена значений для *keyName* . Параметр *valueName* для этого параметра является необязательным, если также используется параметр **/f** . |
| /ве | Выполняет запрос для пустых имен значений. |
| /s | Указывает рекурсивный запрос всех подразделов и имен значений. |
| /се `<separator>` | Задает разделитель одиночного значения для поиска в типе имени значения **REG_MULTI_SZ**. Если *Разделитель* не указан, используется значение **\ 0** . |
| /f `<data>` | Указывает данные или шаблон для поиска. Если строка содержит пробелы, используйте двойные кавычки. Если параметр не указан, в качестве шаблона поиска используется подстановочный знак (**&#42;**). |
| /k | Задает поиск только в именах ключей. |
| /d | Задает поиск только в данных. |
| /C | Указывает, что запрос учитывает регистр. По умолчанию запросы не учитывают регистр. |
| /e | Задает возврат только точных совпадений. По умолчанию возвращаются все совпадения. |
| /t `<Type>` | Указывает типы реестра для поиска. Допустимые типы: **REG_SZ**, **REG_MULTI_SZ**, **REG_EXPAND_SZ**, **REG_DWORD**, **REG_BINARY**, **REG_NONE**. Если не указано, выполняется поиск всех типов. |
| /z | Задает включение числового эквивалента для типа реестра в результатах поиска. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Возвращаемые значения для операции с **запросом reg** :

    | Значение | Описание |
    |--|--|
    | 0 | Успешное завершение |
    | 1 | Сбой |

### <a name="examples"></a>Примеры

Чтобы отобразить значение версия значения Name в ключе Хклм\софтваре\микрософт\рескит, введите:

```
reg query HKLM\Software\Microsoft\ResKit /v Version
```

Чтобы отобразить все подразделы и значения в разделе Key Хклм\софтваре\микрософт\рескит\нт\сетуп на удаленном компьютере с именем ABC, введите:

```
reg query \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```

Чтобы отобразить все подразделы и значения типа REG_MULTI_SZ используя в **#** качестве разделителя, введите:

```
reg query HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```

Чтобы отобразить ключ, значение и данные для точных совпадений с учетом регистра в корне HKLM типа данных REG_SZ, введите:

```
reg query HKLM /f SYSTEM /t REG_SZ /c /e
```

Чтобы отобразить ключ, значение и данные, соответствующие **0F** в данных в корневом ключе HKCU типа данных REG_BINARY, введите:

```
reg query HKCU /f 0F /d /t REG_BINARY
```

Чтобы отобразить значения и данные для имен значений NULL (по умолчанию) в разделе HKLM\SOFTWARE, введите:

```
reg query HKLM\SOFTWARE /ve
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
