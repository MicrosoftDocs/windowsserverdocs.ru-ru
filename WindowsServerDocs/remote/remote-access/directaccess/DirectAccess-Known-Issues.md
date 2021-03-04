---
title: DirectAccess известные проблемы
description: В этом разделе содержится ссылка на документы технической поддержки Майкрософт для DirectAccess в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 3511a91f-1d5d-45a0-97f2-3fc0d6f079b4
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 27df40396e497c409f67be487e5ceb52c335fb00
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101833467"
---
# <a name="directaccess-known-issues"></a>DirectAccess известные проблемы

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2019

## <a name="dns-registration-of-directaccess-client-ipv6-addresses"></a>Регистрация DNS клиентских IPv6-адресов DirectAccess

Начиная с Windows 10 может 2020 обновление, клиент больше не регистрирует свои IP-адреса на DNS-серверах, настроенных в таблица политики разрешения имен (NRPT).
Если требуется регистрация DNS, например " **Управление**", ее можно явно включить с помощью этого раздела реестра на клиенте:

Путь: `HKLM\System\CurrentControlSet\Services\Dnscache\Parameters`<br/>
Тип: `DWORD`<br/>
Имя значения: `DisableNRPTForAdapterRegistration`<br/>
Значения:<br/>
`1` -Регистрация DNS отключена (по умолчанию, так как обновление Windows 10 может 2020)<br/>
`0` -Регистрация DNS включена

## <a name="recommended-hotfixes-and-updates-for-windows-server-2012-directaccess"></a>Рекомендуемые исправления и обновления для DirectAccess Windows Server 2012
Ниже приведена ссылка на документы технической поддержки Майкрософт для DirectAccess, которые необходимо просмотреть и применить перед началом развертывания, чтобы избежать непригодной для использования конфигурации.

-   [Рекомендуемые исправления и обновления для DirectAccess Windows Server 2012](https://support.microsoft.com/kb/2883952)


