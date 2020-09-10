---
title: Microsoft Server Performance Advisor
description: Microsoft Server Performance Advisor
ms.assetid: 468ebcb3-9eaf-477c-ab10-e3f1b3ce63dc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.topic: article
ms.openlocfilehash: bd359e71cfb48ecd8aab24a8538369622dd1d271
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627701"
---
# <a name="microsoft-server-performance-advisor"></a>Microsoft Server Performance Advisor

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Загрузите советник по производительности Microsoft Server (SPA) для диагностики проблем с производительностью в Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 или Windows Server 2008. SPA создает комплексные диагностические отчеты и диаграммы и предоставляет рекомендации, которые помогут быстро анализировать проблемы и разрабатывать корректирующие действия.

-   [Обзор советника по производительности сервера](#bkmk-aboutspa)

-   [Загрузка советника по производительности сервера](#bkmk-downloadspa)

-   [Руководство пользователя по Server Performance Advisor](server-performance-advisor-users-guide.md)

-   [Руководство по разработке пакетов Server Performance Advisor](server-performance-advisor-pack-development-guide.md)

## <a name="overview-of-server-performance-advisor"></a><a href="" id="bkmk-aboutspa"></a>Обзор советника по производительности сервера

Советник по производительности сервера состоит из двух частей — платформы SPA и пакетов советника SPA.

### <a name="the-server-performance-advisor-framework"></a>Платформа советника по производительности сервера

Подсистема, отвечающая за сбор данных, назначенных пакетами Advisor, запись собранных данных в базу данных Microsoft SQL Server, создание удобной для ИТ среды для выполнения сценариев для пакетов Advisor и вывод окончательных отчетов. Необходимо установить платформу SPA только в консоли SPA. Консоль SPA может быть установлена на автономном компьютере для удаленного доступа к тестируемым серверам или должна быть установлена на тестируемом сервере.

### <a name="server-performance-advisor-packs"></a>Пакеты Server Performance Advisor

Пакеты советника по работе — это центр всех правил настройки, состоящий из ряда метаданных и файлов скриптов SQL. SPA поставляется со следующими пакетами Advisor:

-   Базовый пакет Advisor для ОС анализирует производительность общих функций операционной системы, независимо от специализированных серверных ролей.

-   Пакет советника по Internet Information Server (IIS) отслеживает производительность IIS.

-   Пакет советника по Hyper-V анализирует общую производительность роли сервера Hyper-V.

    **Примечание** . Пакет советника по Hyper-V не анализирует гостевые операционные системы.



-   Пакет советника по Active Directory анализирует общую производительность роли Active Directory.

SPA также предлагает расширяемую модель для разработчиков, написанных не корпорацией Майкрософт, для написания пакетов Advisor в соответствии со своими потребностями.

**Примечание** . SPA не может понять все контексты сценариев оборудования и пользователей. Следует использовать рекомендации, предоставляемые средством, для принятия решений и анализа последствий любых потенциальных изменений, вносимых на серверы.



## <a name="download-server-performance-advisor"></a><a href="" id="bkmk-downloadspa"></a>Загрузка советника по производительности сервера


Используйте следующие ссылки для загрузки советника по производительности сервера для Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 или Windows Server 2008:

-   [Советник по производительности Microsoft Server 3,1 (32-разрядный)](https://go.microsoft.com/fwlink/p/?linkid=327751)

-   [Советник по производительности Microsoft Server 3,1 (64-разрядный)](https://go.microsoft.com/fwlink/p/?linkid=327752)

Файлы в CAB-файле можно извлечь с помощью следующих команд:

-   для версии x86: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_x86.cab`

-   для версии x64: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_amd64.cab`

**Внимание!** При извлечении CAB-файла SPA необходимо сохранить иерархическую структуру каталогов для правильной работы. В зависимости от того, какие средства CAB установлены на сервере, извлечение может привести к неработоспособной структуре каталогов. Чтобы хранить иерархическую структуру каталогов, можно использовать служебную программу извлечения CAB-файлов, которая извлекает структуру каталоговых каталогов.

Если средство извлечения CAB-файлов правильно извлекли файлы, вложенные папки будут автоматически отображаться в папке назначения извлечения.

### <a name="spa-prerequisites"></a>Предварительные требования

Для консоли SPA необходимо установить следующее программное обеспечение:

-   Microsoft .NET Framework 4

-   SQL Server 2008 R2 Express SP1 или Microsoft SQL Server 2008 R2 SP1

Более новые версии могут быть совместимыми. Будут отмечены все известные проблемы совместимости продукта с консолью SPA.
