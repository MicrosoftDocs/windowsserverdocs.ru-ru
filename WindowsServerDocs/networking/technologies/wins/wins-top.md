---
title: Служба WINS
description: В этом разделе содержатся сведения о списании WINS и использовании DNS для служб разрешения имен в сети.
manager: brianlic
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: d11daadc107ba604ba1ed61613de049fe339a946
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829173"
---
#  <a name="windows-internet-name-service-wins"></a>Служба WINS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

WINS — это традиционная служба регистрации и разрешения имен компьютеров, которая сопоставляет NetBIOS-имена компьютеров с IP-адресами.

Если вы еще не развернули службу WINS в вашей сети, не развертывайте WINS-сервер, а затем разверните DNS службы доменных имен \( \) . Служба DNS также предоставляет службы регистрации и разрешения имен компьютеров и включает множество дополнительных преимуществ по сравнению с WINS, например интеграцию со службами домен Active Directory.

Дополнительные сведения см. в разделе [Служба доменных имен (DNS)](../../dns/dns-top.md) .

Если вы уже развернули службу WINS в сети, рекомендуется развернуть DNS, а затем списать службу WINS.