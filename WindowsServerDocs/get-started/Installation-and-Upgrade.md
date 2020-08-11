---
title: Обновление и установка Windows Server
description: Как выполнить установку, обновление или миграцию на более новую версию Windows Server.
ms.date: 05/14/2019
ms.topic: article
ms.assetid: 98f876bd-63ff-4c3a-95d4-a8dd8d0d119c
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 4a51fbe19722f381407803e2d8ba1e876898ccce
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959692"
---
# <a name="windows-server-installation-and-upgrade"></a>Установка и обновление Windows Server

>Применяется к: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ищете Windows Server 2019? Ознакомьтесь с разделом [Установка | Обновление | Миграция в Windows Server 2019](../get-started-19/install-upgrade-migrate-19.md).

> [!IMPORTANT]
> Расширенная поддержка Windows Server 2008 R2 и Windows Server 2008 закончится в январе 2020 года. [Узнайте больше о вариантах обновления](#upgrading-from-windows-server-2008-r2-or-windows-server-2008).

Пришло время перейти на более новую версию Windows Server? В зависимости от того, какая операционная система сейчас установлена на вашем компьютере, у вас есть множество вариантов.

## <a name="installation"></a>Установка

Если вы хотите перейти на более новую версию Windows Server на том же оборудовании, единственным способом, который всегда работает, является **чистая установка**. То есть вы просто устанавливаете более новую операционную систему поверх старой на имеющемся у вас оборудовании, удаляя таким образом предыдущую операционную систему. Это самый простой способ, но для начала вам необходимо создать резервную копию данных и запланировать переустановку приложений. Существует несколько факторов, которые следует учитывать, например, требования к системе. Поэтому обязательно проверьте данные по [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303418(v=ws.11)) и [Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)).

При переходе с любой предварительной версии (например, Windows Server 2016 Technical Preview) на выпущенную версию (Windows Server 2016) всегда требуется чистая установка.

## <a name="migration-recommended-for-windows-server-2016"></a>Миграция (рекомендуется для Windows Server 2016)

Документация по миграции Windows Server помогает перенести одну роль или компонент за раз с исходного компьютера, работающего под управлением Windows Server, на другой целевой компьютер, работающий под управлением Windows Server такой же или более новой версии. Для этих целей миграция определяется как перемещение одной роли или компонента и его данных на другой компьютер без обновления компонентов на том же компьютере. Это рекомендуемый способ, при котором перемещаются существующие рабочая нагрузка и данные на более новую версию Windows Server. Чтобы начать работу, проверьте [матрицу миграции и обновления роли сервера](https://go.microsoft.com/fwlink/?LinkId=828595) для Windows Server.

## <a name="cluster-os-rolling-upgrade"></a>Последовательное обновление ОС кластера
Новая функция в Windows Server 2016, которая позволяет администратору обновлять ОС узлов кластера с Windows Server 2012 R2 до Windows Server 2016, не останавливая рабочие нагрузки Hyper-V или масштабируемого файлового сервера. Эта функция позволяет избежать простоя, который может нарушать соглашения об уровне обслуживания. Подробнее эта новая функция рассматривается в статье [Последовательное обновление ОС кластера](../failover-clustering/cluster-operating-system-rolling-upgrade.md).

## <a name="license-conversion"></a>Преобразование лицензии
Для некоторых версий ОС можно перейти с определенного выпуска версии на другой выпуск той же версии за один шаг с помощью простой команды и соответствующего лицензионного ключа. Это называется **преобразованием лицензии**. Например, если ваш сервер работает под управлением Windows Server 2016 Standard, вы можете преобразовать его в Windows Server 2016 Datacenter. В некоторых выпусках Windows Server можно также свободно выбирать переход на оригинальную версию, версию с корпоративным лицензированием и розничную версию с помощью той же команды и соответствующего ключа.

## <a name="upgrade"></a>Обновление с более ранней версии:
Если вы хотите сохранить существующее оборудование и все роли сервера, которые вы настроили, без сжатия сервера, **обновление с более ранней версии** является подходящим вариантом, и для этого существует множество способов. При классическом обновлении вы переходите с более старой операционной системы на более новую, сохраняя свои параметры, роли сервера и данные. Например, если сервер работает под управлением Windows Server 2012 R2, его можно обновить до Windows Server 2016. Однако не каждая устаревшая операционная система позволяет перейти на любую новую ОС.

>[!NOTE]
>Обновление лучше всего работает на виртуальных машинах, где для успешного обновления не нужны специальные драйверы оборудования OEM.

Вы можете провести обновление с ознакомительной версии операционной системы на розничную, с более старой розничной версии на более новую или, в некоторых случаях, с корпоративного выпуска ОС на обычный.

Прежде чем начать обновление, изучите таблицы на этой странице, чтобы узнать, как перейти с имеющейся у вас ОС на более новую.

Дополнительные сведения о различиях между вариантами установки, доступными для Windows Server 2016 Technical Preview, включая компоненты, устанавливаемые в каждом случае, и параметры управления, доступные после установки, приведены на странице [Документация по Windows Server](https://go.microsoft.com/fwlink/?LinkId=828598).

>[!NOTE]
>При миграции или обновлении до любой версии Windows Server следует просмотреть и понять [политику сроков поддержки](https://support.microsoft.com/lifecycle) и период времени для этой версии и плана соответственно. Вы можете [найти информацию о сроках](https://support.microsoft.com/lifecycle) для определенного выпуска Windows Server, который вас интересуют.


## <a name="upgrading-to-windows-server-2016"></a>Обновление до Windows Server 2016
Дополнительные сведения, в том числе важные замечания и ограничения, относящиеся к обновлению, преобразованию лицензий между выпусками Windows Server 2016 и преобразованию ознакомительных выпусков на розничные, приведены в разделе [Параметры обновления и преобразования для Windows Server2016](https://go.microsoft.com/fwlink/?LinkId=828602).

>[!NOTE]
>Примечание. Обновления, переключающиеся с установки основных серверных компонентов на режим "Сервер с рабочим столом" (или наоборот), не поддерживаются. Если более старая операционная система, которую вы обновляете или преобразовываете, является установкой Server Core, результатом по-прежнему будет установка Server Core более новой операционной системы.

Ниже приведена краткая справочная таблица поддерживаемых путей обновления более старых розничных выпусков Windows Server до розничных выпусков Windows Server 2016.


|Если вы используете эти версии и выпуски:|Доступно обновление до этих версий и выпусков:|
|--------------------------------|---------------------------------------|
|Windows Server 2012 Standard|Windows Server 2016 Standard или Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard или Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Hyper-V Server 2012 R2|Hyper-V Server 2016 (с использованием функции последовательного обновления ОС кластера)|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 Workgroup|

### <a name="license-conversion"></a>Преобразование лицензии
Вы можете перейти с Windows Server 2016 Standard (розничная версия) на Windows Server 2016 Datacenter (розничная версия).

Вы можете перейти с Windows Server 2016 Essentials (розничная версия) на Windows Server 2016 Standard (розничная версия).

Вы можете перейти с ознакомительной версии Windows Server 2016 Standard, Windows Server 2016 Standard (розничная версия) либо Datacenter (розничная версия).

Вы можете перейти с ознакомительной версии Windows Server 2016 Datacenter на Windows Server 2016 Datacenter (розничная версия).

## <a name="upgrading-to-windows-server-2012-r2"></a>Обновление до Windows Server 2012 R2
Дополнительные сведения, в том числе важные замечания и ограничения, относящиеся к обновлению, преобразованию лицензий между выпусками Windows Server 2012 R2 и преобразованию ознакомительных выпусков на розничные, приведены в разделе [Upgrade Options for Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) (Варианты обновления Windows Server 2012 R2).

Ниже приведена краткая справочная таблица поддерживаемых путей обновления более старых розничных выпусков Windows Server до розничных выпусков Windows Server 2012 R2.

|Используемая версия|Доступно обновление до следующих выпусков|
|-------------------------|---------------------------|
|Windows Server 2008 R2 Datacenter с пакетом обновления 1 (SP1)|Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Enterprise с пакетом обновления 1 (SP1)|Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter|
|Windows Server 2008 R2 Standard с пакетом обновления 1 (SP1)|Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter|
|Windows Web Server 2008 R2 с пакетом обновления 1 (SP1)|Windows Server 2012 R2 Standard|
|Windows Server 2012 Datacenter|Windows Server 2012 R2 Datacenter|
|Windows Server 2012 Standard|Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter|
|Hyper-V Server 2012|Hyper-V Server 2012 R2|

### <a name="license-conversion"></a>Преобразование лицензии
Вы можете перейти с Windows Server 2012 Standard (розничная версия) на Windows Server 2012 Datacenter (розничная версия).

Вы можете перейти с Windows Server 2012 Essentials (розничная версия) на Windows Server 2012 Standard (розничная версия).

Вы можете перейти с ознакомительной версии Windows Server 2012 Standard на Windows Server 2012 Standard (розничная версия) либо Windows Server 2012 Datacenter (розничная версия).

## <a name="upgrading-to-windows-server-2012"></a>Обновление до Windows Server 2012
Дополнительные сведения, в том числе важные замечания и ограничения, относящиеся к обновлению и преобразованию ознакомительных версий в розничные, приведены в разделе [Evaluation Versions and Upgrade Options for Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574204(v=ws.11)) (Ознакомительные версии и варианты обновления Windows Server 2012).

Ниже приведена краткая справочная таблица поддерживаемых путей обновления более старых розничных выпусков Windows Server до розничных выпусков Windows Server 2012.

|Используемая версия|Доступно обновление до следующих выпусков|
|--------------------------|--------------------------|
|Windows Server 2008 Standard с SP2 или Windows Server 2008 Enterprise с SP2|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 Datacenter с пакетом обновления 2 (SP2)|Windows Server 2012 Datacenter|
|Windows Web Server 2008|Windows Server 2012 Standard|
|Windows Server 2008 R2 Standard с пакетом обновления 1 (SP1) или Windows Server 2008 R2 Enterprise с пакетом обновления 1 (SP1)|Windows Server 2012 Standard, Windows Server 2012 Datacenter|
|Windows Server 2008 R2 Datacenter с пакетом обновления 1 (SP1)|Windows Server 2012 Datacenter|
|Windows Web Server 2008 R2|Windows Server 2012 Standard|

### <a name="license-conversion"></a>Преобразование лицензии
Вы можете перейти с Windows Server 2012 Standard (розничная версия) на Windows Server 2012 Datacenter (розничная версия).

Вы можете перейти с Windows Server 2012 Essentials (розничная версия) на Windows Server 2012 Standard (розничная версия).

Вы можете перейти с ознакомительной версии Windows Server 2012 Standard на Windows Server 2012 Standard (розничная версия) либо Windows Server 2012 Datacenter (розничная версия).

## <a name="upgrading-from-windows-server-2008-r2-or-windows-server-2008"></a>Обновление Windows Server 2008 R2 или Windows Server 2008

Как описано в разделе [Обновление Windows Server 2008 и Windows Server 2008 R2](modernize-windows-server-2008.md), расширенная поддержка Windows Server 2008 R2 и Windows Server 2008 заканчивается в январе 2020 года. Чтобы обеспечить отсутствие перерывов в поддержке, необходимо выполнить обновление до поддерживаемой версии Windows Server или осуществить повторное размещение в Azure, перейдя на [специализированные виртуальные машины Windows Server 2008 R2](uploading-specialized-WS08-image-to-azure.md). Ознакомьтесь с [руководством по миграции для Windows Server](https://go.microsoft.com/fwlink/?linkid=872689), чтобы получить сведения и рекомендации по планированию миграции или обновления.

Для локальных серверов не предусмотрен прямой путь обновления Windows Server 2008 R2 до Windows Server 2016 или более поздней версии. Вместо этого сначала обновите их до Windows Server 2012 R2, а затем — [до Windows Server 2016](#upgrading-to-windows-server-2016).

При планировании обновления учитывайте приведенные ниже рекомендации по промежуточному шагу обновления до Windows Server 2012 R2.

  - Невозможно выполнить обновление на месте 32-разрядной архитектуры до 64-разрядной архитектуры или сборки одного типа до сборки другого типа (например, сборки fre до chk).

  - Обновление на месте поддерживаются только для того же языка. Невозможно выполнить обновление с одного языка на другой.

  - Невозможно перейти с Windows Server 2008 с установленными основными серверными компонентами на Windows Server 2012 R2 с графическим пользовательским интерфейсом сервера (Windows Server с возможностями рабочего стола). Вы можете перейти с обновленной установки основных серверных компонентов на сервер с возможностями рабочего стола, но только в Windows Server 2012 R2. Windows Server 2016 и более поздние версии *не* поддерживают переход с установки основных серверных компонентов на сервер с возможностями рабочего стола, поэтому его нужно выполнить перед обновлением до Windows Server 2016.

Чтобы получить дополнительные сведения, ознакомьтесь с разделом [Evaluation Versions and Upgrade Options for Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj574204\(v=ws.11\)) (Ознакомительные версии и варианты обновления Windows Server 2012), содержащим информацию об обновлении ролей.
