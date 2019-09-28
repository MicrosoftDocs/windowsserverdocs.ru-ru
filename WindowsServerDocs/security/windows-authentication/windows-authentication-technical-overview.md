---
title: Технический обзор проверки подлинности Windows
description: Безопасность Windows Server
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 286d3e41-434f-4703-9320-706d06ebda51
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: f2916bc9c3654f0e5e3d4dc27ce79874fdb863f7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403262"
---
# <a name="windows-authentication-technical-overview"></a>Технический обзор проверки подлинности Windows

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе для ИТ Professional содержатся ссылки на статьи, посвященные техническим обзору проверки подлинности Windows. Проверка подлинности Windows — это процесс, подтверждающий подлинность пользователя или службы, пытающейся получить доступ к Windows.

В этой коллекции разделов описывается архитектура проверки подлинности Windows и ее компоненты.

Чтобы сохранить в цифровом виде или распечатать страницы из этой библиотеки, нажмите кнопку **Экспорт** (в правом верхнем углу страницы) и следуйте инструкциям.

-   [Различия в проверке подлинности Windows между операционными системами Windows](https://technet.microsoft.com/library/dn169017.aspx)

    Описание существенных различий в архитектуре проверки подлинности и процессах.

-   [Основные понятия проверки подлинности Windows](https://technet.microsoft.com/library/dn169018.aspx)

    Описывает основные понятия, на которых основана проверка подлинности Windows.

-   [Сценарии проверки подлинности входа Windows](https://technet.microsoft.com/library/dn169020.aspx)

    Содержит сводку различных сценариев входа в систему.

-   [Архитектура проверки подлинности Windows](https://technet.microsoft.com/library/dn169024.aspx)

    Описание существенных различий в архитектуре проверки подлинности и процессах для операционных систем Windows.

    -   [Архитектура интерфейса поставщика поддержки безопасности](https://technet.microsoft.com/library/dn169026.aspx)

        Описывает архитектуру SSPI.

    -   [Процедуры с учетными данными в проверке подлинности Windows](https://technet.microsoft.com/library/dn169014.aspx)

        Описание различных процессов управления учетными данными.

-   [Групповые политики, используемые при проверке подлинности Windows](https://technet.microsoft.com/library/dn169021.aspx)

    Описывает использование и влияние групповых политик в процессе проверки подлинности.

## <a name="what-is-not-covered"></a>Что не охватывается
В этой коллекции разделов не рассматриваются процедуры проектирования, реализации и мониторинга технологий проверки подлинности в среде Windows.

-   Сведения о стратегиях авторизации Windows см. в статье [Разработка стратегии авторизации ресурсов](https://technet.microsoft.com/library/cc783368.aspx).

-   Сведения о проектировании стратегии проверки подлинности Windows см. в разделе [Разработка стратегии проверки подлинности](https://technet.microsoft.com/library/cc758124.aspx).

-   Сведения о стратегиях реализации инфраструктуры открытых ключей Windows см. в разделе [Разработка инфраструктуры открытых ключей](https://technet.microsoft.com/library/cc773138.aspx).

-   Сведения о настройке и мониторинге безопасности, включая проверку подлинности, в среде Windows см. в следующих статьях:

    -   [Руководством по безопасности Windows XP](https://www.microsoft.com/download/details.aspx?id=962)

    -   [Базовые показатели безопасности Windows Vista](https://technet.microsoft.com/library/dd450978.aspx)

    -   [Базовые показатели безопасности Windows Server 2003](https://technet.microsoft.com/library/cc163140.aspx) и [рекомендации по угрозам и контрмерам](https://technet.microsoft.com/library/dd162275.aspx)

    -   [Рекомендации по безопасности Windows Server 2008](https://www.microsoft.com/download/details.aspx?id=17606)

    -   [Базовые показатели безопасности Windows Server 2008 R2](https://technet.microsoft.com/library/gg236605.aspx)

-   Сведения о аудите событий входа и проверки подлинности в Windows см. в разделе [Audit Security Events](https://technet.microsoft.com/library/cc776394.aspx).


