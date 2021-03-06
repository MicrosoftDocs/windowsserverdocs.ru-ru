---
title: Убедитесь, что драйвер виртуальной функции работает правильно, если виртуальная машина настроена для использования SR-IOV
description: Узнайте, что делать, если драйвер виртуальной функции работает неправильно в гостевой операционной системе одной или нескольких виртуальных машин.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
ms.date: 8/16/2016
ms.openlocfilehash: a009060dc67ba29c12e986167b2ed746865311d5
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845911"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>Убедитесь, что драйвер виртуальной функции работает правильно, если виртуальная машина настроена для использования SR-IOV

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство|Сведения|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Предупреждение|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>Проблема
*Драйвер виртуальной функции работает неправильно в гостевой операционной системе одной или нескольких виртуальных машин.*

## <a name="impact"></a>Влияние
*Производительность сети не является оптимальной для следующих виртуальных машин:*

\<list of virtual machines>

## <a name="resolution"></a>Решение
*В операционной системе на виртуальной машине выполните следующие действия. Убедитесь, что установлены соответствующие драйверы и все сетевые устройства включены, а также проверьте наличие ошибок или предупреждений в журнале событий.*



