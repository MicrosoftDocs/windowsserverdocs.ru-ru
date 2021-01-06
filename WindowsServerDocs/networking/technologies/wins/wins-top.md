---
title: Служба WINS
description: В этом разделе содержатся сведения о списании WINS и использовании DNS для служб разрешения имен в сети.
manager: brianlic
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: b512df968dcaee068ce014a1ec59e86aacbac812
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947430"
---
#  <a name="windows-internet-name-service-wins"></a>Служба WINS

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

WINS — это традиционная служба регистрации и разрешения имен компьютеров, которая сопоставляет NetBIOS-имена компьютеров с IP-адресами.

Если вы еще не развернули службу WINS в вашей сети, не развертывайте WINS-сервер, а затем разверните DNS службы доменных имен \( \) . Служба DNS также предоставляет службы регистрации и разрешения имен компьютеров и включает множество дополнительных преимуществ по сравнению с WINS, например интеграцию со службами домен Active Directory.

Дополнительные сведения см. в разделе [Служба доменных имен (DNS)](../../dns/dns-top.md) .

Если вы уже развернули службу WINS в сети, рекомендуется развернуть DNS, а затем списать службу WINS.