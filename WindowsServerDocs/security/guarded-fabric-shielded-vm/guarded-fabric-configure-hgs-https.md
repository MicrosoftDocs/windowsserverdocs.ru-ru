---
title: Настройка HGS для обмена данными по протоколу HTTPS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 4e708b61bd629b5b784926338b1aee122e2ecbee
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966161"
---
# <a name="configure-hgs-for-https-communications"></a>Настройка HGS для обмена данными по протоколу HTTPS

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

По умолчанию при инициализации сервера HGS он настраивает веб-сайты IIS для обмена данными только по протоколу HTTP.
Все конфиденциальные материалы, передаваемые и из HGS, всегда шифруются с помощью шифрования на уровне сообщений. Однако если требуется более высокий уровень безопасности, можно также включить протокол HTTPS, настроив для HGS SSL-сертификат.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)]

