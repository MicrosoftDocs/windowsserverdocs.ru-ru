---
title: Команду scwcmd, представление
description: Справочная статья для * * * *-
ms.topic: reference
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 985b8edb2ef6a99abeb9545dfe62fa5255080b2c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636900"
---
# <a name="scwcmd-view"></a>Scwcmd: view

> Область применения: Windows Server 2012 R2, Windows Server 2012

Визуализирует XML-файл с помощью указанного преобразования XSL. Эта команда может быть полезной для отображения файлов мастера настройки безопасности (SCW). XML с использованием различных представлений.

## <a name="syntax"></a>Синтаксис

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

#### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|/x\<Xmlfile.xml>|Указывает XML-файл для просмотра. Этот параметр должен быть указан.|
|ключ\<Xslfile.xsl>|Указывает преобразование XSL, применяемое к XML-файлу как часть процесса отрисовки. Этот параметр является необязательным для файлов SCW. XML. Если команда **View** используется для отображения файла SCW. XML, она автоматически попытается загрузить правильное преобразование по умолчанию для указанного XML-файла. Если задано преобразование XSL, преобразование должно быть написано с учетом предположения, что XML-файл находится в том же каталоге, что и преобразование XSL.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Примечания

Scwcmd.exe доступны только на компьютерах под управлением Windows Server 2008 R2, Windows Server 2008 или Windows Server 2003.

## <a name="examples"></a>Примеры

Чтобы просмотреть Policyfile.xml с помощью преобразования Полицивиев. xsl, введите:
```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)