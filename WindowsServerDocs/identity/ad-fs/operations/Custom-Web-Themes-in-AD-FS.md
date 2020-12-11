---
description: Дополнительные сведения о пользовательских веб-темах см. в AD FS
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: Пользовательские веб-темы в AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 303d1903be5a21d35abe2724401d73170673751c
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039942"
---
# <a name="custom-web-themes-in-ad-fs"></a>Пользовательские веб-темы в AD FS

Тема, которая поставляется \- из \- \- комплекта, называется по умолчанию. Можно экспортировать тему по умолчанию и воспользоваться ей, чтобы быстро приступить к работе. Можно настроить внешний вид и поведение, включая настройку макета (путем изменения CSS-файла), импортировать и применить эту новую тему, а затем работать с настроенными внешним видом и поведением. Использование CSS-файла упрощает взаимодействие с веб-дизайнерами.

Следующий командлет позволяет создать пользовательскую веб-тему, дублирующую веб-тему по умолчанию.

```powershell
New-AdfsWebTheme –Name custom –SourceName default
```

Можно изменить CSS-файл и настроить новую веб-тему с помощью нового CSS-файла. Для экспорта веб-темы воспользуйтесь следующим командлетом.

```powershell
Export-AdfsWebTheme –Name default –DirectoryPath c:\theme
```

Для применения CSS-файла к новой теме воспользуйтесь следующим командлетом.

```powershell
Set-AdfsWebTheme –TargetName custom –StyleSheet @{path="c:\NewTheme.css"}
```

Следующий командлет позволяет создать пользовательскую веб-тему из новой таблицы стилей.

```powershell
New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"} –RTLStyleSheetPath c:\NewRtlTheme.css
```

Чтобы применить пользовательскую веб-тему к AD FS, используйте следующий командлет.

```powershell
Set-AdfsWebConfig -ActiveThemeName custom
```

Чтобы добавить JavaScript в AD FS, используйте следующий командлет.

```powershell
Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=' /adfs/portal/script/onload.js';path="D:\inetpub\adfsassets\script\onload.js"}
```

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
