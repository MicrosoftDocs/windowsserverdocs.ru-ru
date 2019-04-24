---
title: Не устанавливайте обслуживания хранилища, при использовании разностный виртуальный жесткий диск, когда родительские и дочерние виртуальные жесткие диски находятся на разных томах
description: Интернет-версию текст для этого правила анализатора соответствия рекомендациям.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2bdc8462c4d9dc50dbb69792f2f294add0ca3a74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856205"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>Не устанавливайте обслуживания хранилища, при использовании разностный виртуальный жесткий диск, когда родительские и дочерние виртуальные жесткие диски находятся на разных томах

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и проверках см. в разделе [запуска наиболее проверок анализатором соответствия рекомендациям и Управление результатами проверок](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукта или компонента**|Hyper-V|  
|**Уровень серьезности**|Предупреждение|  
|**Категория**|Конфигурация|  
  
В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.
  
## <a name="issue"></a>**Проблема**  
*Разностный виртуальный жесткий диск с родительским и дочерним виртуальными жесткими дисками на разных томах имеет обслуживания хранилища включена.*  
  
## <a name="impact"></a>**Влияние**  
*Эта конфигурация может привести непредвиденный хранилища поведение качества обслуживания для разностный виртуальный жесткий диск, а также других виртуальных жестких дисков на томах родительской и дочерней. Это влияет на следующие виртуальные жесткие диски:*  
  
\<Список виртуальных жестких дисков >  
  
## <a name="resolution"></a>**Решение**  
*Отключить обслуживания хранилища для упоминаемой виртуальных жестких дисков, или выполнить миграцию хранилища для перемещения в том же родительским и дочерним виртуальным жестким диском.*  
  

