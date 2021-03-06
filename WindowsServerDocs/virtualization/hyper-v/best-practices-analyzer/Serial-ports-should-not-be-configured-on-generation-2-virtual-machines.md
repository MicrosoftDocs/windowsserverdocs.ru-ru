---
title: Не следует настраивать последовательные порты на виртуальных машинах поколения 2
description: Интернет-версия текста для этого правила анализатор соответствия рекомендациям.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
ms.date: 8/16/2016
ms.openlocfilehash: 2dbb9aae488922daeff74242d74d38685a371497
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744109"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>Не следует настраивать последовательные порты на виртуальных машинах поколения 2

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство.|Подробнее|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Предупреждение|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>**Проблема**
*Для одной или нескольких виртуальных машин поколения 2 настроен последовательный порт.*

## <a name="impact"></a>**Влияние**
*Производительность может затронуть следующие виртуальные машины:*

\<list of virtual machines>

## <a name="resolution"></a>**Решение**
*Если это сделано намеренно, дальнейшие действия не требуются. В противном случае рассмотрите возможность использования диспетчера Hyper-V или Windows PowerShell для удаления строки подключения из последовательных портов на виртуальной машине.*



