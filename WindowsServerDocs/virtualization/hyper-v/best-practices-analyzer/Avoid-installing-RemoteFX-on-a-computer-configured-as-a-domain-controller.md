---
title: Избегайте установки RemoteFX на компьютере, который настроен в качестве контроллера домена Active Directory
description: Интернет-версия текста для этого правила анализатор соответствия рекомендациям.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
ms.date: 8/16/2016
ms.openlocfilehash: 1f639998c568035d0c992403cd0b1056ea4607b5
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/17/2020
ms.locfileid: "90747059"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Избегайте установки RemoteFX на компьютере, который настроен в качестве контроллера домена Active Directory

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство.|Подробнее|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Ошибка|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>**Проблема**
*RemoteFX устанавливается на контроллере домена.*

## <a name="impact"></a>**Влияние**
*Виртуальные компьютеры, настроенные для RemoteFX, не могут использоваться на этих компьютерах.*

## <a name="resolution"></a>**Решение**
*Решите, следует ли настроить этот сервер с помощью RemoteFX для Hyper-V или в качестве контроллера домен Active Directory, а затем при необходимости перенастройте сервер.*



