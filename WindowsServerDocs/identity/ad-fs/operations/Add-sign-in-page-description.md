---
description: 'Дополнительные сведения: Добавление описания страницы входа'
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: Добавление описания страницы входа
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ff74a70bf0ef55798f48bd871b180de5cc792f75
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044272"
---
# <a name="add-sign-in-page-description"></a>Добавить \- Описание страницы входа

## <a name="to-add-sign-in-page-description"></a>Добавление \- описания страницы входа
Чтобы добавить \- Описание страницы входа на \- страницу входа, используйте следующий командлет и синтаксис Windows PowerShell.

![добавить описание входа](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

```powershell
Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"
```

> [!IMPORTANT]
> Строка для параметра `SignInPageDescriptionText` поддерживает чистый HTML-код с тегами и без них. Таким образом, можно также выполнить следующий командлет, не используя &lt; тег p &gt; .  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." `

Когда страница входа \- настроена, настройка имеет приоритет, поэтому следует настроить для всех языков, которые требуется поддерживать. Все настроенное содержимое принимает параметр, определяющий языковой стандарт. При настройке локализованного содержимого перед настройкой \- региональных стандартов страны и региона, \- например "en US", необходимо сначала настроить страну меньше языкового стандарта, например "en" \- .

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
