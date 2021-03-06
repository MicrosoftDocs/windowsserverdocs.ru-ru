---
description: 'Дополнительные сведения о: Добавление ссылки на службу поддержки'
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: Добавление ссылки на службу технической поддержки
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c806390687d5293feacd2575b10569504334914f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044372"
---
# <a name="add-help-desk-link"></a>Добавление ссылки на службу технической поддержки


## <a name="to-add-a-help-desk-link"></a>Добавление ссылки службы поддержки
Чтобы добавить ссылку службы поддержки, которая отображается на \- странице входа, используйте следующий командлет и синтаксис Windows PowerShell.

![Добавить службу поддержки](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`


> [!IMPORTANT]
> Параметр `linkText` в этом командлете не является обязательным, за исключением случаев использования значения, отличного от значения по умолчанию — *Help* (справка). Преимущество использования значения по умолчанию — локализация на все языковые стандарты клиента. После настройки страницы входа вступают в силу пользовательские настройки. Следовательно, необходимо выполнить пользовательскую настройку для всех языков, которые требуется поддерживать.


## <a name="additional-references"></a>Дополнительная справка
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
