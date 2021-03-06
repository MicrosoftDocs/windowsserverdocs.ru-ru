---
title: Предотвращение приостановки работы виртуальной машины
description: Сведения о том, что делать, если на сервере имеется одна или несколько виртуальных машин в приостановленном состоянии.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
ms.date: 8/16/2016
ms.openlocfilehash: c1f5ba73a181ef0ec89dfa83bdbb82b3b49e9c6d
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834619"
---
# <a name="avoid-pausing-a-virtual-machine"></a>Предотвращение приостановки работы виртуальной машины

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

*Этот сервер имеет одну или несколько виртуальных машин в приостановленном состоянии.*

## <a name="impact"></a>Влияние

*В зависимости от объема доступной памяти может оказаться невозможным запуск дополнительных виртуальных машин.*

Приостановленные виртуальные машины не освобождают выделенную память. Это означает, что память недоступна для запуска других виртуальных машин.

## <a name="resolution"></a>Решение

*Если это сделано намеренно, дальнейшие действия не требуются. В противном случае попробуйте возобновить работу этих виртуальных машин или выключить их.*

#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Возобновление работы виртуальной машины с помощью диспетчера Hyper-V

1.  Откройте диспетчер Hyper-V. (В меню **сервис** Диспетчер сервера выберите пункт **Диспетчер Hyper-V**.)

2.  В списке **виртуальные машины** найдите виртуальные машины с состоянием **приостановлено**.

    > [!IMPORTANT]
    > Состояние " **приостановлено — критическое** " возникает, когда на физическом хранилище для этой виртуальной машины остается очень мало свободного места. Прежде чем попытаться возобновить работу виртуальной машины в этом состоянии, освободите место в физическом хранилище.

3.  Щелкните правой кнопкой мыши имя каждой виртуальной машины и выберите пункт **возобновить**. После этого виртуальная машина возобновит работу. После этого, если вы хотите завершить работу виртуальной машины, щелкните ее правой кнопкой мыши и выберите пункт **Завершение работы**.

#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Возобновление работы виртуальной машины с помощью Windows PowerShell

Это можно сделать в одной команде, используя фильтрацию и конвейер после того, как вы получите все виртуальные машины на узле. Тип:

```
get-vm | where state -eq 'paused' | resume-vm
```



