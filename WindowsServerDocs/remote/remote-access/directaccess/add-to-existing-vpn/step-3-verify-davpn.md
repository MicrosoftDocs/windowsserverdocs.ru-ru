---
title: Шаг 3. Проверка развертывания
description: Эта статья является частью инструкции по добавлению DirectAccess в существующее развертывание удаленного доступа (VPN) для Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43ac612e-2e77-418c-8171-ebb2086b7cb6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3967f50a354ee6ed31273734f2449d6d337d9b50
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314726"
---
# <a name="step-3-verify-the-deployment"></a>Шаг 3. Проверка развертывания

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описывается, как проверить правильность настройки развертывания DirectAccess.  
  
### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>Проверка доступа к внутренним ресурсам с помощью DirectAccess  
  
1.  Подключите клиентский компьютер с DirectAccess к корпоративной сети и получите групповую политику.  
  
2.  В области уведомлений щелкните значок **Сетевые подключения** , чтобы получить доступ к диспетчеру мультимедиа DA.  
  
3.  Щелкните **Подключение DirectAccess**. Будет отображено состояние подключения — **Подключено локально**.  
  
4.  Подключите клиентский компьютер к внешней сети и попытайтесь получить доступ к внутренним ресурсам.  
  
    Вам должны быть доступны все корпоративные ресурсы.  
  


