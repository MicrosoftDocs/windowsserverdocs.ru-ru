---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: Изменение названия компании на странице входа AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e47d0ee6b1969bca847dd88bfc6cca69bd72b6ba
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956581"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Изменение названия компании на странице входа AD FS

Чтобы изменить имя компании, отображаемое на \- странице входа, используйте следующий командлет и синтаксис Windows PowerShell. Это значение настраивается по умолчанию с помощью значения из отображаемого имени службы федерации, вводимого во время настройки.

![изменить имя](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)

```powershell
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"
```

> [!NOTE]
> Можно также использовать интегрированную среду сценариев Windows PowerShell \( \) для изменения названия компании. С помощью интегрированной среды сценариев Windows PowerShell можно отображать содержимое в среде, \- совместимой с Юникодом. Дополнительные сведения см. в разделе [Знакомство с Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).

## <a name="additional-references"></a>Дополнительная справка

- [AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
