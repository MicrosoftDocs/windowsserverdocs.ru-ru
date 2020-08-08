---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: Настройка для локализации
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 41a540b43fde264718ca7aa81ba0e48184cf1265
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956391"
---
# <a name="customization-for-localization"></a>Настройка для локализации

Возможна локализация веб-содержимого на языки, отличные от английского. При локализации необходимо обращать внимание на следующие аспекты.

После настройки содержимого вступают в силу пользовательские настройки. Следовательно, необходимо выполнить пользовательскую настройку для всех языков, которые требуется поддерживать. Все настроенное содержимое принимает параметр, определяющий языковой стандарт. При настройке локализованного содержимого настройте его с использованием страны \- меньшего языкового стандарта, например "en", перед настройкой страны и региона, \- относящихся к региону, например "en \- US".

Ниже показаны некоторые дополнительные примеры кода.

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}
Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}
```

Ниже показаны некоторые дополнительные примеры кода.

```powershell
Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"

Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"
```

Если вы хотите настроить веб-содержимое на языках, отличных от английского, для которых требуется ввод данных в Юникоде, рекомендуется использовать интегрированную среду сценариев Windows PowerShell. Дополнительные сведения см. [в статье Знакомство с интегрированной средой сценариев Windows PowerShell](/previous-versions/mt707506(v=msdn.10)).

## <a name="additional-references"></a>Дополнительная справка

[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
