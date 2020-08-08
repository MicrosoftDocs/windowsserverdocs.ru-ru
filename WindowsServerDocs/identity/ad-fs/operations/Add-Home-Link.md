---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Добавление ссылки на домашнюю страницу
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4bd64d19f5e203086c4a5576f331fde9d1b33cf7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954290"
---
# <a name="add-home-link"></a>Добавление ссылки на домашнюю страницу

Чтобы добавить ссылку Home, которая отображается на \- странице входа, используйте следующий командлет и синтаксис Windows PowerShell.


![Добавить домашнюю ссылку](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home `


> [!IMPORTANT]
> Параметр `linkText` в этом командлете не является обязательным, за исключением случаев использования значения, отличного от значения по умолчанию — *Home* (главная). Преимущество использования значения по умолчанию — локализация на все языковые стандарты клиента. Когда страница входа \- настроена, настройка имеет приоритет, поэтому следует настроить для всех языков, которые требуется поддерживать.

## <a name="additional-references"></a>Дополнительная справка
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
