---
title: Зарезервировать один или несколько внешних виртуальных сетей для монопольного использования виртуальными машинами
description: Инструкции для устранения проблемы, о которых сообщает это правило анализатора соответствия рекомендациям.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f7732258-93f1-44e8-835b-5ad2d1c45cd9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c8c90a74352bae0b348608db0fc05107e4d09010
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884745"
---
# <a name="reserve-one-or-more-external-virtual-networks-for-exclusive-use-by-virtual-machines"></a>Зарезервировать один или несколько внешних виртуальных сетей для монопольного использования виртуальными машинами

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Анализатор соответствия рекомендациям](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукта или компонента**|Hyper-V|  
|**Уровень серьезности**|Ошибка|  
|**Категория**|Конфигурация|  
  
В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.  
  
## <a name="issue"></a>Проблемы  
  
*Все внешние виртуальные сети настроены для использования с виртуальных машин и управления операционной системы.*  
  
## <a name="impact"></a>Влияние  
  
*Производительность сети могут быть ограничены в управляющей операционной системе.*  
  
## <a name="resolution"></a>Разрешение  
  
*Позволяет отменить общий доступ к внешней виртуальной сети с управляющей операционной системе диспетчер виртуальных коммутаторов.*  
  
#### <a name="to-stop-sharing-the-external-virtual-network-with-the-management-operating-system"></a>Чтобы отменить общий доступ к внешней виртуальной сети с помощью операционной системы  
  
1.  Откройте диспетчер Hyper-V. Нажмите кнопку **запустить**, пункты **Администрирование**, а затем нажмите кнопку **диспетчера Hyper-V**.  
  
2.  В меню **Действия** выберите пункт **Диспетчер виртуальных коммутаторов**.  
  
3.  В разделе **виртуальные коммутаторы**, щелкните имя внешний виртуальный коммутатор.  
  
4.  В **тип подключения** области рядом с именем физический сетевой адаптер, снимите **разрешить управляющей операционной системе совместно использовать этот сетевой адаптер** "флажок".  
  
5.  Нажмите кнопку **ОК**.  
  

