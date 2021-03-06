---
title: Использовать все виртуальные функции для работы в сети, если они доступны
description: Узнайте, что делать, если не используются некоторые возможности аппаратного ускорения.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
ms.date: 8/16/2016
ms.openlocfilehash: 4252fd790c34bb9f4eca116eff84eb900033658b
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846307"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>Использовать все виртуальные функции для работы в сети, если они доступны

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
*Некоторые возможности аппаратного ускорения не используются*

## <a name="impact"></a>Влияние
*Эта конфигурация может привести к тому, что общая загрузка ЦП будет выше, чем требуется. Производительность сети может быть неоптимальной на следующих виртуальных машинах:*

\<list of virtual machines>

## <a name="resolution"></a>Решение
*Рассмотрите возможность настройки виртуального сетевого адаптера для SR-IOV, если физическое оборудование поддерживает SR-IOV, и если эта конфигурация не конфликтует с сетевыми компонентами, необходимыми для виртуальной машины.*



