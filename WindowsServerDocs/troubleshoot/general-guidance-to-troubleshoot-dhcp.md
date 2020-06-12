---
title: Общие рекомендации по устранению неполадок DHCP
description: В этом артилцее представлены общие рекомендации по устранению неполадок DHCP.
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: c0460791fef2451722af09e8bbe08b51a605f01b
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150162"
---
# <a name="general-guidance-to-troubleshoot-dhcp"></a>Общие рекомендации по устранению неполадок DHCP

Прежде чем начать устранение неполадок, проверьте следующие элементы. Они могут помочь найти основную причину проблемы.

## <a name="checklist"></a>Контрольный список

  - Когда появилась проблема?

  - Есть ли какие либо сообщения об ошибках?

  - Был ли DHCP-сервер запущен ранее или он никогда не работал?  
    Если он работал ранее, все изменилось до начала проблемы. Например, было ли установлено обновление? Было ли сделано изменение в инфраструктуре?

  - Проблема является постоянной или временной? Если это нерегулярное время, когда она была выполнена в последний раз?

  - Происходят ли ошибки аренды адресов для всех клиентов или только для конкретных клиентов, например подсеть с одной областью?

  - Есть ли клиенты в той же сетевой подсети, что и DHCP-сервер?

  - Если клиенты находятся в одной подсети, могут ли они получить IP-адреса?

  - Если клиенты находятся в разных сетевых подсетях, то правильно ли настроены маршрутизаторы или коммутаторы виртуальной ЛС для работы агентов ретранслятора DHCP (также известных как вспомогательные службы IP)?

  - Является ли DHCP-сервер автономным или настроен для обеспечения высокой доступности, например разделения области или отработки отказа DHCP?

  - Проверьте промежуточные устройства на наличие таких функций, как VRRP/HSRP, динамическая проверка ARP или отслеживание DHCP, которые вызывают проблемы.