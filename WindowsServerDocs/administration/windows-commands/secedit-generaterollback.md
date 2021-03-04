---
title: secedit generaterollback
description: Справочная статья по команде secedit женератероллбакк, которая позволяет создать шаблон отката для указанного шаблона конфигурации.
ms.topic: reference
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b433cda07e3555fd46d12c055e36444a267a88cf
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806167"
---
# <a name="secedit-generaterollback"></a>Secedit/женератероллбакк

Позволяет создать шаблон отката для указанного шаблона конфигурации. Если существует существующий шаблон отката, то при повторной попытке выполнения этой команды существующие данные будут перезаписаны.

Успешное выполнение этой команды записывает в журнал несоответствия между указанным шаблоном безопасности и конфигурацией политики безопасности в файле Scesrv. log.

## <a name="syntax"></a>Синтаксис

```
secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /DB | Обязательный элемент. Указывает путь и имя файла базы данных, содержащей хранимую конфигурацию, для которой выполняется анализ. Если имя файла указывает базу данных, для которой не был связан шаблон безопасности (представленный файлом конфигурации), `/cfg <configuration file name>` необходимо также указать параметр. |
| /CFG | Обязательный элемент. Указывает путь и имя файла для шаблона безопасности, который будет импортирован в базу данных для анализа. Этот параметр допустим только при использовании с `/db <database file name>` параметром. Если этот параметр также не указан, анализ выполняется для любой конфигурации, уже хранящейся в базе данных. |
| /рбк | Обязательный элемент. Указывает шаблон безопасности, в который записываются сведения об откате. Шаблоны безопасности создаются с помощью оснастки "Шаблоны безопасности". С помощью этой команды можно создать файлы отката. |
| /log | Указывает путь и имя файла журнала, который будет использоваться в процессе. Если не указать расположение файла, используется файл журнала по умолчанию `<systemroot>\Documents and Settings\<UserAccount>\My Documents\Security\Logs\<databasename>.log` . |
| /quiet | Подавляет вывод на экран и журнал. Вы по-прежнему можете просматривать результаты анализа с помощью оснастки "Настройка и анализ безопасности" консоли управления (MMC). |

## <a name="examples"></a>Примеры

Чтобы создать файл конфигурации отката для ранее созданного файла *сектмплконтосо. INF* , сохранив исходные параметры, а затем записать действие в файл журнала *SecAnalysisContosoFY11* , введите:

```
secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Secedit/Analyze](secedit-analyze.md)

- [Secedit/configure](secedit-configure.md)

- [Secedit/Export](secedit-export.md)

- [Secedit/Import](secedit-import.md)

- [Secedit/Validate](secedit-validate.md)