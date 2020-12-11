---
description: 'Дополнительные сведения: DNS и AD DS'
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS и доменные службы Active Directory
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: a61b5dd3c0150c7f293425acb3ca948f8acd51f8
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97050192"
---
# <a name="dns-and-ad-ds"></a>DNS и доменные службы Active Directory

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Службы домен Active Directory Services (AD DS) используют службы разрешения имен системы доменных имен (DNS), чтобы клиенты могли искать контроллеры домена и контроллеры домена, на которых размещается служба каталогов, для взаимодействия друг с другом.

AD DS позволяет легко интегрировать пространство имен Active Directory в существующее пространство имен DNS. Такие функции, как интегрированные с Active Directory зоны DNS, упрощают развертывание DNS, устраняя необходимость в настройке дополнительных зон, а затем настраивают зонные передачи.

Сведения о том, как DNS поддерживает AD DS, см. в разделе [поддержка DNS для Active Directory технического справочника](/previous-versions/windows/it-pro/windows-server-2003/cc781627(v=ws.10)).

> [!NOTE]
> При реализации несвязанного пространства имен, в котором доменное имя AD DS отличается от основного DNS-суффикса, который используется клиентами, AD DS интеграция с DNS является более сложной. Дополнительные сведения см. в разделе несвязанное [пространство имен](Disjoint-Namespace.md).

## <a name="in-this-section"></a>В этом разделе

- [Расположение контроллера домена](Domain-Controller-Location.md)
- [Зоны DNS, интегрированные с Active Directory](Active-Directory-Integrated-DNS-Zones.md)
- [Именование компьютеров](Computer-Naming.md)
- [Несвязанное пространство имен](Disjoint-Namespace.md)
