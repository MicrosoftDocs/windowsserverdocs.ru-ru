---
title: prndrvr
description: Справочная статья по команде прндрвр, которая добавляет, удаляет и перечисляет драйверы принтера.
ms.topic: reference
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a3ddb87346009f50b8956d5ce1cd1367c82e7f72
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101808139"
---
# <a name="prndrvr"></a>prndrvr

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет, удаляет и перечисляет драйверы принтера. Эта команда представляет собой Visual Basic сценарий, расположенный в `%WINdir%\System32\printing_Admin_Scripts\<language>` каталоге. Чтобы использовать эту команду в командной строке, введите **cscript** , а затем полный путь к файлу прндрвр или измените каталоги на соответствующую папку. Например: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr`.

При использовании без параметров **прндрвр** отображает справку командной строки.

## <a name="syntax"></a>Синтаксис

```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] [-e <environment>] [-s <Servername>] [-u <Username>] [-w <password>] [-h <path>] [-i <inf file>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -a | Устанавливает драйвер. |
| -d | Удаляет драйвер. |
| -l | Список всех драйверов принтеров, установленных на сервере, заданном параметром **-s** . Если сервер не указан, Windows выводит список драйверов принтера, установленных на локальном компьютере. |
| -X | Удаляет все драйверы принтеров и дополнительные драйверы принтеров, которые не используются логическим принтером на сервере, указанном параметром **-s** . Если не указать сервер для удаления из списка, Windows удалит все неиспользуемые драйверы принтеров на локальном компьютере. |
| -m `<model_name>` | Указывает (по имени) драйвер, который вы хотите установить. Драйверы часто называются для модели поддерживаемых принтеров. Дополнительные сведения см. в документации принтера. |
| `-v {0|1|2|3}` | Указывает версию драйвера, который вы хотите установить. Сведения о том, какие версии доступны для какой среды, см. в описании параметра **-e**. Если не указать версию, будет установлена версия драйвера, соответствующая версии Windows, установленной на компьютере, на котором устанавливается драйвер. |
| -e `<environment>` | Указывает среду для драйвера, который вы хотите установить. Если среда не указана, используется среда компьютера, на котором устанавливается драйвер. Поддерживаются следующие параметры среды: **Windows NT x86**, **Windows x64** или **Windows ia64**. |
| -s `<Servername>` | Указывает имя удаленного компьютера, на котором размещен принтер, которым требуется управлять. Если компьютер не указан, используется локальный компьютер. |
| -u `<Username>` -w `<password>` | Указывает учетную запись с разрешениями на подключение к компьютеру, на котором размещен принтер, которым требуется управлять. Все члены локальной группы администраторов целевого компьютера имеют эти разрешения, но разрешения также могут быть предоставлены другим пользователям. Если учетная запись не указана, для работы команды необходимо войти в систему с учетной записью с этими разрешениями. |
| -h `<path>` | Указывает путь к файлу драйвера. Если путь не указан, используется путь к расположению, где установлена операционная система Windows. |
| -i `<filename.inf>` | Указывает полный путь и имя файла драйвера, который вы хотите установить. Если не указать имя файла, сценарий использует один из файлов входящих INF-файла принтера в подкаталоге INF каталога Windows.<p>Если путь к драйверу не указан, сценарий выполняет поиск файлов драйверов в файле driver.cab. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Если предоставленные сведения содержат пробелы, заключите его в кавычки (например, "имя компьютера").

- Параметр **-x** удаляет все дополнительные драйверы принтера (драйверы, установленные для использования на клиентах под управлением альтернативных версий Windows), даже если основной драйвер используется. Если компонент факса установлен, этот параметр также удаляет драйверы факсов. Основной драйвер факса удаляется, если он не используется (т. е. Если с ним нет очереди). Если основной драйвер факса удален, то единственным способом повторного включения факса является повторная установка компонента факса.

### <a name="examples"></a>Примеры

Чтобы получить список всех драйверов на локальном \\ сервере printServer1, введите:

```
cscript prndrvr -l -s
```

Чтобы добавить драйвер принтера Windows x64 версии 3 для модели лазерного принтера модель принтера 1, используя информационный файл драйвера c:\temp\Laserprinter1.inf для драйвера, хранящегося в папке c:\temp, введите:

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64 -i c:\temp\Laserprinter1.inf -h c:\temp
```

Чтобы удалить драйвер принтера Windows x64 версии 3 для модели лазерного принтера 1, введите:

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам системы печати](print-command-reference.md)
