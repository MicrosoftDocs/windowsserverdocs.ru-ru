---
title: secedit analyze
description: Справочная статья по команде secedit Analyze, которая позволяет анализировать текущие системные настройки по базовым параметрам, хранящимся в базе данных.
ms.topic: reference
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1fd730b50b306110244d58552174dab5f976814d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806227"
---
# <a name="secedit-analyze"></a>Secedit/Analyze

Позволяет анализировать текущие системные параметры по базовым параметрам, хранящимся в базе данных.

## <a name="syntax"></a>Синтаксис

```
secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /DB | Обязательный элемент. Указывает путь и имя файла базы данных, содержащей хранимую конфигурацию, для которой выполняется анализ. Если имя файла указывает базу данных, для которой не был связан шаблон безопасности (представленный файлом конфигурации), `/cfg <configuration file name>` необходимо также указать параметр. |
| /CFG | Указывает путь и имя файла для шаблона безопасности, который будет импортирован в базу данных для анализа. Этот параметр допустим только при использовании с `/db <database file name>` параметром. Если этот параметр также не указан, анализ выполняется для любой конфигурации, уже хранящейся в базе данных. |
| /overwrite | Указывает, должен ли шаблон безопасности в параметре **/CFG** перезаписывать любой шаблон или составной шаблон, хранящийся в базе данных, вместо того, чтобы добавлять результаты в сохраненный шаблон. Этот параметр допустим только в том случае, если `/cfg <configuration file name>` параметр также используется. Если этот параметр также не указан, шаблон в параметре **/CFG** добавляется к сохраненному шаблону. |
| /log | Указывает путь и имя файла журнала, который будет использоваться в процессе. Если не указать расположение файла, используется файл журнала по умолчанию `<systemroot>\Documents and Settings\<UserAccount>\My Documents\Security\Logs\<databasename>.log` . |
| /quiet | Подавляет вывод на экран. Вы по-прежнему можете просматривать результаты анализа с помощью оснастки "Настройка и анализ безопасности" консоли управления (MMC). |

## <a name="examples"></a>Примеры

Чтобы выполнить анализ параметров безопасности в базе данных безопасности *секдбконтосо. sdb*, а затем направить выходные данные в файл *SecAnalysisContosoFY11*, включая запросы на проверку правильности выполнения команды, введите:

```
secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

Чтобы внести изменения, необходимые для процесса анализа в файле *секконтосо. INF* , а затем направить выходные данные в существующий файл, *SecAnalysisContosoFY11* без запроса, введите:

```
secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Secedit/configure](secedit-configure.md)

- [Secedit/Export](secedit-export.md)

- [Secedit/женератероллбакк](secedit-generaterollback.md)

- [Secedit/Import](secedit-import.md)

- [Secedit/Validate](secedit-validate.md)