---
title: Повторная синхронизация репликации должна быть запланирована на часы наименьшей нагрузки
description: Узнайте, что делать, если повторная синхронизация репликации для основных виртуальных машин не запланирована в часы наименьшей нагрузки.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
ms.date: 8/16/2016
ms.openlocfilehash: 3669abf4da79db82d0ba7ca985b886a02a180ea9
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845810"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>Повторная синхронизация репликации должна быть запланирована на часы наименьшей нагрузки

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство|Сведения|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Предупреждение|
|**Категория**|Операции|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>Проблема
*Повторная синхронизация репликации для основных виртуальных машин не запланирована в часы наименьшей нагрузки.*

## <a name="impact"></a>Влияние
*Чем дольше виртуальная машина находится в состоянии, которое требует повторной синхронизации, тем дольше увеличивается размер файлов журналов репликации, а на основных виртуальных машинах происходят более Нереплицируемые изменения. Это влияет на следующие виртуальные машины:*

\<list of virtual machines>

## <a name="resolution"></a>Решение
*С помощью диспетчера Hyper-V измените параметры репликации для виртуальной машины, чтобы она автоматически выполняла синхронизацию в часы наименьшей нагрузки.*



