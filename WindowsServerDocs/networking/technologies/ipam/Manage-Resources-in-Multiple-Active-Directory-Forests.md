---
title: Управление ресурсами в нескольких лесах Active Directory
description: Узнайте, как использовать IPAM для управления контроллерами домена, DHCP-серверами и DNS-серверами в нескольких Active Directory лесах.
manager: brianlic
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 23b60402833c5df97882de35909425edaff93d9d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830169"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>Управление ресурсами в нескольких лесах Active Directory

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела вы узнаете, как использовать IPAM для управления контроллерами домена, DHCP-серверами и DNS-серверами в нескольких Active Directory лесах.

Чтобы использовать IPAM для управления ресурсами в удаленных Active Directory лесах, каждый лес, которым требуется управлять, должен иметь двустороннее отношение доверия с лесом, в котором установлена система IPAM.

Чтобы начать процесс обнаружения для разных лесов Active Directory, откройте диспетчер сервера и щелкните IPAM. В консоли клиента IPAM щелкните **Настройка обнаружения сервера**, а затем — **получить леса**. Это инициирует фоновую задачу, которая обнаруживает доверенные леса и их домены. После завершения процесса обнаружения нажмите кнопку **настроить обнаружение сервера**, чтобы открыть следующее диалоговое окно.

![Настройка обнаружения серверов](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)

>[!NOTE]
>Для групповая политика \- подготовки на основе Active Directory сценария с перекрестным лесом убедитесь, что на сервере IPAM выполняется следующий командлет Windows PowerShell, а не контроллер домена-доверия. Например, если IPAM-сервер присоединен к лесу corp.contoso.com, а доверенный лес — fabrikam.com, можно выполнить следующий командлет Windows PowerShell на сервере IPAM в corp.contoso.com для \- подготовки на основе групповая политика в лесу Fabrikam.com. Для выполнения этого командлета необходимо быть членом группы "Администраторы домена" в лесу fabrikam.com.

```powershell
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
```

В диалоговом окне **Настройка обнаружения сервера** щелкните **выбрать лес**, а затем выберите лес, которым требуется управлять с помощью IPAM. Также выберите домены, которыми требуется управлять, и нажмите кнопку **Добавить**.

В окне **Выбор ролей сервера для обнаружения** для каждого домена, которым требуется управлять, укажите тип серверов для обнаружения. Доступны такие параметры, как **контроллер домена**, **DHCP-сервер** и **DNS-сервер**.

По умолчанию обнаруживаются контроллеры домена, DHCP-серверы и DNS-серверы. Если вы не хотите обнаруживать один из этих типов серверов, снимите флажок для этого параметра.

На приведенном выше примере IPAM-сервер устанавливается в лес contoso.com, а для управления IPAM добавляется корневой домен леса fabrikam.com. Выбранные роли сервера позволяют IPAM обнаруживать контроллеры домена, DHCP-серверы и DNS-серверы, а также управлять ими в корневом домене fabrikam.com и корневом домене contoso.com.

После указания лесов, доменов и ролей сервера нажмите кнопку **ОК**. IPAM выполняет обнаружение. После завершения обнаружения можно управлять ресурсами как в локальном, так и в удаленном лесу.
