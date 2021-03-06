---
title: динамическая память включена, но не отвечает на некоторых виртуальных машинах
description: Узнайте, что делать, если на одной или нескольких виртуальных машинах возникают проблемы с драйвером, необходимым для динамическая память в гостевой операционной системе.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
ms.date: 8/16/2016
ms.openlocfilehash: 2fbf600e2fa06f01ddbf3ad3dafc02ded25dc6fc
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846108"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>динамическая память включена, но не отвечает на некоторых виртуальных машинах

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
*На одной или нескольких виртуальных машинах возникли проблемы с драйвером, необходимым для динамическая память в гостевой операционной системе.*

## <a name="impact"></a>Влияние
*Гостевая операционная система на следующих виртуальных машинах может не запускаться или работать ненадежно, так как Hyper-V не может динамически настроить память для реагирования на изменения в требованиях к памяти. Это влияет на следующие виртуальные машины:*

\<list of virtual machines>

## <a name="resolution"></a>Решение
*Это ожидаемое поведение, если виртуальная машина загружается. Если виртуальная машина не загружается, убедитесь, что службы Integration Services обновлены до последней версии и что операционная система на виртуальной машине поддерживает динамическая память.*

Начиная с Windows Server 2016, службы Integration Services доставляются через Центр обновления Windows. Убедитесь, что виртуальные машины настроены на получение обновлений для получения последней версии служб Integration Services.

Динамическая память работает с конкретными версиями поддерживаемых гостевых систем. Дополнительные сведения о версиях, предшествующих Windows Server 2016 и Windows 10, см. в статье [обзор Динамическая память Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831766(v=ws.11)) .