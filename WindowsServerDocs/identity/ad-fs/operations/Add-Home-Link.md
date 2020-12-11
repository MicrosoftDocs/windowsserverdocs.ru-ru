---
description: 'Дополнительные сведения о: Добавление домашней ссылки'
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Добавление ссылки на домашнюю страницу
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 5f684ae3e68459721678a50c91cc04d58c89d81c
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039352"
---
# <a name="add-home-link"></a>Добавление ссылки на домашнюю страницу

Чтобы добавить ссылку Home, которая отображается на \- странице входа, используйте следующий командлет и синтаксис Windows PowerShell.


![Добавить домашнюю ссылку](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home `


> [!IMPORTANT]
> Параметр `linkText` в этом командлете не является обязательным, за исключением случаев использования значения, отличного от значения по умолчанию — *Home* (главная). Преимущество использования значения по умолчанию — локализация на все языковые стандарты клиента. Когда страница входа \- настроена, настройка имеет приоритет, поэтому следует настроить для всех языков, которые требуется поддерживать.

## <a name="additional-references"></a>Дополнительная справка
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
