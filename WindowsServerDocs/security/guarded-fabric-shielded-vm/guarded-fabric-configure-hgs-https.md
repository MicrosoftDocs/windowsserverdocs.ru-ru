---
description: Дополнительные сведения см. в статье Настройка HGS для обмена данными по протоколу HTTPS.
title: Настройка HGS для обмена данными по протоколу HTTPS
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: c28500d236625410961ef1ee3012001c1d277714
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049892"
---
# <a name="configure-hgs-for-https-communications"></a>Настройка HGS для обмена данными по протоколу HTTPS

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

По умолчанию при инициализации сервера HGS он настраивает веб-сайты IIS для обмена данными только по протоколу HTTP.
Все конфиденциальные материалы, передаваемые и из HGS, всегда шифруются с помощью шифрования на уровне сообщений. Однако если требуется более высокий уровень безопасности, можно также включить протокол HTTPS, настроив для HGS SSL-сертификат.

[!INCLUDE [Configure HTTPS](../../../includes/configure-hgs-for-https.md)]

