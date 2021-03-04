---
title: Шаг 3. Проверка развертываний
description: Узнайте, как убедиться, что вы правильно настроили базовое развертывание DirectAccess.
manager: brianlic
ms.topic: article
ms.assetid: 45e9edd6-acca-4d59-851a-a0cc8bd8b4c6
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 7ed58bbfae65762fd315777497dcc7aac610bd13
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101827548"
---
# <a name="step-3-verify-deployments"></a>Шаг 3. Проверка развертываний

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе содержатся сведения о проверке правильности настройки базового развертывания DirectAccess.

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>Проверка доступа к внутренним ресурсам с помощью DirectAccess

1.  Подключите клиентский компьютер с DirectAccess к корпоративной сети и получите групповую политику.

2.  В области уведомлений щелкните значок **Сетевые подключения**, чтобы получить доступ к диспетчеру мультимедиа DA.

3.  Щелкните **Подключение DirectAccess**. Будет отображено состояние подключения — **Подключено локально**.

4.  Подключите клиентский компьютер к внешней сети и попытайтесь получить доступ к внутренним ресурсам.

    Вам должны быть доступны все корпоративные ресурсы.

## <a name="previous-step"></a><a name="BKMK_Links"></a>Предыдущий шаг

-   [Шаг 2. Настройка сервера DirectAccess](da-basic-configure-s2-server.md)



