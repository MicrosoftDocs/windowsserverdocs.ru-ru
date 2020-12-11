---
description: 'Подробнее: изменение логотипа компании на странице входа AD FS'
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: Изменение логотипа компании на странице входа AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.openlocfilehash: a04f7a81c26dea4234fbb92edc44125ae11e51f6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040282"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Изменение логотипа компании на странице входа AD FS

## <a name="change-company-logo"></a>Изменение логотипа компании

Чтобы изменить эмблему компании, отображаемую на \- странице входа, используйте следующий командлет PowerShell Windows PowerShell и синтаксис.

![изменить логотип](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> Рекомендуемые размеры логотипа — 260 x 35 @ 96 точек на дюйм. Размер файла не должен превышать 10 КБ.

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}
```

> [!NOTE]
> Параметр `TargetName` является обязательным. Тема по умолчанию, которая выпускается с AD FS, называется *Default*.

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
