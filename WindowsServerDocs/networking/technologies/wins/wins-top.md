---
title: Служба WINS
description: В этом разделе содержатся сведения о списании WINS и использовании DNS для служб разрешения имен в сети.
manager: brianlic
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 36dc2b0e8bbb6b65b0cc3568641017aa51122650
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955501"
---
#  <a name="windows-internet-name-service-wins"></a>Служба WINS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

WINS — это традиционная служба регистрации и разрешения имен компьютеров, которая сопоставляет NetBIOS-имена компьютеров с IP-адресами.

Если вы еще не развернули службу WINS в вашей сети, не развертывайте WINS-сервер, а затем разверните DNS службы доменных имен \( \) . Служба DNS также предоставляет службы регистрации и разрешения имен компьютеров и включает множество дополнительных преимуществ по сравнению с WINS, например интеграцию со службами домен Active Directory.

Дополнительные сведения см. в разделе [Служба доменных имен (DNS)](https://docs.microsoft.com/windows-server/networking/dns/dns-top) .

Если вы уже развернули службу WINS в сети, рекомендуется развернуть DNS, а затем списать службу WINS.
