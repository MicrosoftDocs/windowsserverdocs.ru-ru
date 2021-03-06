---
title: Настройка виртуальной машины с контроллером SCSI для возможности горячего подключения и горячей замены хранилища
description: Узнайте, что делать, если обнаружена виртуальная машина, для которой не настроен SCSI-контроллер.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
ms.date: 8/16/2016
ms.openlocfilehash: b56f0e7beae706471c829810bea023dbcab2317c
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2020
ms.locfileid: "97833549"
---
# <a name="configure-a-virtual-machine-with-a-scsi-controller-to-be-able-to-hot-plug-and-hot-unplug-storage"></a>Настройка виртуальной машины с контроллером SCSI для возможности горячего подключения и горячей замены хранилища

>Область применения. Windows Server 2016



*Дополнительные сведения о рекомендациях и проверках см. в разделе* [анализатор соответствия рекомендациям](https://go.microsoft.com/fwlink/?LinkId=122786).

|Свойство|Сведения|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Предупреждение|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>Проблема

*Обнаружена виртуальная машина, для которой не настроен SCSI-контроллер.*

## <a name="impact"></a>Влияние

*Вы не сможете использовать горячее подключение или горячее отключение хранилища для следующих виртуальных машин:*

\<list of virtual machine names>

Возможность горячего подключения или горячего отключения хранилища упрощает управление потребностями в хранении виртуальной машины, не требуя простоев. Прежде чем можно будет добавлять или удалять хранилище, виртуальные машины без контроллеров SCSI должны быть выключены.

## <a name="resolution"></a>Решение

*Если для этой виртуальной машины не требуется горячая установка или горячее отключение хранилища, никаких действий не требуется. В противном случае завершите работу виртуальной машины и добавьте контроллер SCSI в конфигурацию.*

Для использования контроллера SCSI с горячим подключением и горячим отключением хранилища на гостевой операционной системе должна быть установлена текущая версия служб Integration Services.



