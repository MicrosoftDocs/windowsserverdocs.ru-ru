---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: Отказоустойчивая кластеризация
ms.prod: windows-server
ms.topic: landing-page
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 06/06/2019
ms.localizationpriority: high
ms.openlocfilehash: 5b0193f18fe94f391f1bbbc41280c16e4a1bcd0c
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203495"
---
# <a name="failover-clustering-in-windows-server"></a>Отказоустойчивая кластеризация в Windows Server

> Применяется к: Windows Server 2019, Windows Server 2016

Отказоустойчивый кластер — это группа независимых компьютеров, которые работают совместно в целях повышения доступности и масштабируемости кластерных ролей (ранее называемых кластерными приложениями и службами). Кластерные серверы (называемые "узлы") соединены физическими кабелями и программным обеспечением. При сбое на одном из узлов кластера его функции немедленно передаются другим узлам (этот процесс называется отработкой отказа). Кроме того, за кластерными ролями ведется профилактическое наблюдение, чтобы обеспечить их правильную работу. Если они не работают, выполняется перезагрузка или перемещение на другой узел.

Отказоустойчивые кластеры также предоставляют функции общего тома кластера (CSV), которые образуют согласованное распределенное пространство имен, используемое кластерными ролями для доступа к общему хранилищу со всех узлов. Благодаря функции отказоустойчивой кластеризации пользователи сталкиваются с минимальным количеством проблем в работе службы.

Отказоустойчивая кластеризация имеет много возможностей практического применения, в том числе следующие:

* Высокодоступное или постоянно доступное хранилище файловых ресурсов общего доступа для приложений, таких как Microsoft SQL Server и виртуальные машины Hyper-V.
* Высокодоступные кластерные роли, выполняемые на физических серверах или виртуальных машинах, установленных на серверах, на которых выполняется Hyper-V.

| **Общие сведения**                                                               |  **Планирование**                          |  **Развертывание**       |
| -------------                                                                |  --------------                        | --------------------- |
| [Что нового в отказоустойчивой кластеризации?](whats-new-in-failover-clustering.md)    | [Планирование требований к оборудованию для отказоустойчивой кластеризации и варианты хранилища](clustering-requirements.md)  | [Создание отказоустойчивого кластера](create-failover-cluster.md) |
| [Масштабируемый файловый сервер для данных приложений](sofs-overview.md)               | [Использование общих томов кластера (CSV)](failover-cluster-csvs.md) | [Развертывание двухузлового файлового сервера](deploy-two-node-clustered-file-server.md) |
|  [Кворум кластеров и пулов](../storage/storage-spaces/understand-quorum.md)   |  [Использование кластеров гостевых виртуальных машин с локальными дисковыми пространствами](../storage/storage-spaces/storage-spaces-direct-in-vm.md)       | [Подготовка кластерных объектов-компьютеров в доменных службах Active Directory](prestage-cluster-adds.md) |
| [Служба сведений о домене сбоя](fault-domains.md)                                 |                                 | [Настройка учетных записей кластеров в Active Directory](configure-ad-accounts.md) |
| [Упрощенные сети кластера SMB Multichannel и Multi-NIC](smb-multichannel.md) |                       | [Управление кворумом и свидетелями](manage-cluster-quorum.md) |
| [Балансировка нагрузки для виртуальных машин](vm-load-balancing-overview.md)                         |                             | [Развертывание облака-свидетеля](deploy-cloud-witness.md) |
| [Наборы кластеров](../storage/storage-spaces/cluster-sets.md)                  |                             |[Развертывание файлового ресурса-свидетеля](file-share-witness.md) |
| [Сходство кластеров](cluster-affinity.md)                                     |                            | [Последовательное обновление ОС кластера](cluster-operating-system-rolling-upgrade.md) |
|                                                                             |                            | [Обновление отказоустойчивого кластера на одном оборудовании](upgrade-option-same-hardware.md) |
|                                                                            |                             | [Развертывание отсоединенного от Active Directory кластера](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\))

|**Управление**  |  **Средства и параметры**  |  **Ресурсы сообщества**       |
| ------------- |  -------------- | --------------------- |
| [Кластерное обновление](cluster-aware-updating.md)    |   [Командлеты PowerShell для отказоустойчивой кластеризации](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)      |  [Форум по кластеризации (высокой доступности)](https://go.microsoft.com/fwlink/p/?LinkId=230641)       |
|  [Служба работоспособности](health-service-overview.md)   |   [Командлеты PowerShell для обновления с поддержкой кластера](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)      | [Блог группы отказоустойчивой кластеризации и балансировки сетевой нагрузки](https://blogs.msdn.com/b/clustering/)        |
|  [Перенос кластера между доменами](cluster-domain-migration.md)   |         |         |
|  [Устранение неполадок с помощью отчетов об ошибках Windows](troubleshooting-using-wer-reports.md)   |         |         |
