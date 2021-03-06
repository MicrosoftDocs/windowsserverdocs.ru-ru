---
title: Общие сведения о контроле учетных записей
description: Узнайте об управлении учетными записями пользователей, о том, как это фундаментальный компонент общей концепции безопасности корпорации Майкрософт и как он помогает уменьшить воздействие вредоносной программы.
ms.topic: article
ms.assetid: 1b7a39cd-fc10-4408-befd-4b2c45806732
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 5ac0ded6d7d44fa1ca7d2a8af966e4d069d3470a
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101832093"
---
# <a name="user-account-control-overview"></a>Общие сведения о контроле учетных записей
Контроль учетных записей пользователей \( \) — это фундаментальный компонент общей концепции безопасности корпорации Майкрософт.  Контроль учетных записей помогает уменьшить влияние вредоносных программ.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Описание функции
UAC позволяет всем пользователям выполнять вход на свой компьютер, используя учетную запись обычного пользователя. Процессы, запущенные с использованием токена обычного пользователя, могут выполнять разные задачи, используя предоставленные обычному пользователю права доступа. К примеру, проводник Windows автоматически наследует разрешения уровня обычного пользователя. Кроме того, все программы, выполняемые с помощью проводника Windows \( , например, двойным \- щелчком ярлыка приложения \) также выполняются со стандартным набором разрешений пользователя. Многие приложения, включая те, которые входят в состав самой операционной системы, спроектированы таким образом, чтобы правильно работать.

Другие приложения, особенно те, которые не были специально разработаны с учетом параметров безопасности, часто нуждаются в дополнительных разрешениях для успешного выполнения. Эти типы программ называются устаревшими приложениями. Кроме того, такие действия, как установка нового программного обеспечения и внесение изменений в конфигурацию таких программ, как брандмауэр Windows, занимают больше разрешений, чем доступно для учетной записи обычного пользователя.

Если приложения должны работать с более чем стандартными правами пользователя, UAC может восстановить дополнительные группы пользователей для маркера. Это позволяет пользователю иметь явный контроль над программами, выполняющими изменения на уровне системы на компьютере или устройстве.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Практическое применение
Режим одобрения администратором в контроле учетных записей помогает предотвратить автоматическую установку вредоносных программ без ведома администратора. Он также помогает защититься от непреднамеренного \- изменения всей системы. Наконец, этот режим можно использовать для принудительного обеспечения более высокого уровня соответствия требованиям, при котором администраторы должны активно выражать свое согласие или предоставлять учетные данные для каждого административного действия.



