---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS и доменные службы Active Directory
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: f531ffc8226fae9f515882e99da4620badc08611
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947713"
---
# <a name="dns-and-ad-ds"></a>DNS и доменные службы Active Directory

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Службы домен Active Directory Services (AD DS) используют службы разрешения имен системы доменных имен (DNS), чтобы клиенты могли искать контроллеры домена и контроллеры домена, на которых размещается служба каталогов, для взаимодействия друг с другом.

AD DS позволяет легко интегрировать пространство имен Active Directory в существующее пространство имен DNS. Такие функции, как интегрированные с Active Directory зоны DNS, упрощают развертывание DNS, устраняя необходимость в настройке дополнительных зон, а затем настраивают зонные передачи.

Сведения о том, как DNS поддерживает AD DS, см. в разделе [поддержка DNS для Active Directory технического справочника](/previous-versions/windows/it-pro/windows-server-2003/cc781627(v=ws.10)).

> [!NOTE]
> При реализации несвязанного пространства имен, в котором доменное имя AD DS отличается от основного DNS-суффикса, который используется клиентами, AD DS интеграция с DNS является более сложной. Дополнительные сведения см. в разделе несвязанное [пространство имен](Disjoint-Namespace.md).

## <a name="in-this-section"></a>Содержание раздела

- [Расположение контроллера домена](Domain-Controller-Location.md)
- [Зоны DNS, интегрированные с Active Directory](Active-Directory-Integrated-DNS-Zones.md)
- [Именование компьютеров](Computer-Naming.md)
- [Несвязанное пространство имен](Disjoint-Namespace.md)
