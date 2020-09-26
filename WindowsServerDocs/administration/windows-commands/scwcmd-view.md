---
title: scwcmd view
description: Справочная статья по команде команду scwcmd view, которая визуализирует XML-файл с помощью указанного преобразования XSL.
ms.topic: reference
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e411bf06015684e7dedb94d109f5e4294f46af84
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388934"
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