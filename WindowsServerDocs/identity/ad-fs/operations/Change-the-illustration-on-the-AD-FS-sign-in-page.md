---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Изменение иллюстрации на странице входа AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 91ba9ca9068ccf2d619c8f98e1f678df7194e1a6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956521"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Изменение иллюстрации на странице входа AD FS

## <a name="change-the-illustration"></a>Изменение иллюстрации

Чтобы изменить иллюстрацию, рисунок слева, отображаемый на \- странице входа, должен использовать следующий командлет и синтаксис Windows PowerShell.

![изменить иллюстрацию](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> Рекомендуемые размеры иллюстрации —1420 x 1080 пикселей @ 96 точек на дюйм. Размер файла не должен превышать 200 КБ.

```powershell
Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}
```

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
