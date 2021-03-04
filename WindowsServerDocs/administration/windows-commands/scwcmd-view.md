---
title: scwcmd view
description: Справочная статья по команде команду scwcmd view, которая визуализирует XML-файл с помощью указанного преобразования XSL.
ms.topic: reference
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b2afa8e43d727333b3bb6db5e8ca3a348e587ee5
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806307"
---
# <a name="scwcmd-view"></a>scwcmd view

> Область применения: Windows Server 2012 R2 и Windows Server 2012

Визуализирует XML-файл с помощью указанного преобразования XSL. Эта команда может быть полезной для отображения файлов мастера настройки безопасности (SCW). XML с использованием различных представлений.

## <a name="syntax"></a>Синтаксис

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| /x`<Xmlfile.xml>` | Указывает XML-файл для просмотра. Этот параметр должен быть указан. |
| ключ`<Xslfile.xsl>` | Указывает преобразование XSL, применяемое к XML-файлу как часть процесса отрисовки. Этот параметр является необязательным для файлов SCW. XML. Если команда **View** используется для отображения файла SCW. XML, она автоматически попытается загрузить правильное преобразование по умолчанию для указанного XML-файла. Если задано преобразование XSL, преобразование должно быть написано с учетом предположения, что XML-файл находится в том же каталоге, что и преобразование XSL. |
| /? | Отображение справки в командной строке. |

## <a name="example"></a>Пример

Чтобы просмотреть *Policyfile.xml* с помощью преобразования *полицивиев. xsl* , введите:

```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда команду scwcmd Analyze](scwcmd-analyze.md)

- [команду scwcmd configure, команда](scwcmd-configure.md)

- [команду scwcmd Register, команда](scwcmd-register.md)

- [команда отката команду scwcmd](scwcmd-rollback.md)

- [Команда преобразования команду scwcmd](scwcmd-transform.md)