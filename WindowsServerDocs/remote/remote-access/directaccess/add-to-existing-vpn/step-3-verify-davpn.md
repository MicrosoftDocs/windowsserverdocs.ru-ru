---
title: Шаг 3. Проверка развертывания с помощью удаленного доступа (VPN)
description: Эта статья является частью инструкции по добавлению DirectAccess в существующее развертывание удаленного доступа (VPN) для Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 43ac612e-2e77-418c-8171-ebb2086b7cb6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9da14f076f177e7e819c1529f9de647b5dde0500
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969221"
---
# <a name="step-3-verify-the-remote-access-vpn-deployment"></a>Шаг 3. Проверка развертывания с помощью удаленного доступа (VPN)

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе описывается, как проверить правильность настройки развертывания DirectAccess.

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>Проверка доступа к внутренним ресурсам с помощью DirectAccess

1.  Подключите клиентский компьютер с DirectAccess к корпоративной сети и получите групповую политику.

2.  В области уведомлений щелкните значок **Сетевые подключения**, чтобы получить доступ к диспетчеру мультимедиа DA.

3.  Щелкните **Подключение DirectAccess**. Будет отображено состояние подключения — **Подключено локально**.

4.  Подключите клиентский компьютер к внешней сети и попытайтесь получить доступ к внутренним ресурсам.

    Вам должны быть доступны все корпоративные ресурсы.



