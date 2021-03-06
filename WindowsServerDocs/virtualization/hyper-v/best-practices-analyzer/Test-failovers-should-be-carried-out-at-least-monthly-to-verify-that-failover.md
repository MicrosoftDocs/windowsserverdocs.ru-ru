---
title: Тестовые отработки отказа должны выполняться по крайней мере ежемесячно, чтобы убедиться, что отработка отказа будет выполнена, а рабочие нагрузки виртуальных машин будут работать так, как ожидалось
description: Узнайте, что делать, если тестовая отработка отказа не выполнялась хотя бы в один месяц.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
ms.date: 8/16/2016
ms.openlocfilehash: bf2b1f8bae67c2303fe19a92ac15a2cfdb46511c
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845839"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>Тестовые отработки отказа должны выполняться по крайней мере ежемесячно, чтобы убедиться, что отработка отказа будет выполнена, а рабочие нагрузки виртуальных машин будут работать так, как ожидалось

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
*Тестовая отработка отказа не пройдена хотя бы в течение одного месяца.*

## <a name="impact"></a>Влияние
*Нет подтверждения о том, что запланированная или незапланированная отработка отказа будет успешно выполнена, а операции рабочей нагрузки будут выполняться правильно после отработки отказа. Это влияет на следующие виртуальные машины:*

\<list of virtual machines>

## <a name="resolution"></a>Решение
*Используйте диспетчер Hyper-V для проведения тестовой отработки отказа.*



