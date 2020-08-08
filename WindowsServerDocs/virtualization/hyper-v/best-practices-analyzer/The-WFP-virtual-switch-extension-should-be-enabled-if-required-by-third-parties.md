---
title: Расширение виртуального коммутатора WFP должно быть включено, если оно требуется для расширений сторонних поставщиков
description: Интернет-версия текста для этого правила анализатор соответствия рекомендациям.
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8aa8a9a5-e3fa-4c9b-8331-ba5a3de22429
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 8a8ee1cae5f1eb64e11494d62bc31ebff295d284
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960477"
---
# <a name="the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions"></a>Расширение виртуального коммутатора WFP должно быть включено, если оно требуется для расширений сторонних поставщиков

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство|Сведения|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Предупреждение|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>**Проблема**
*Расширение виртуального коммутатора платформы фильтрации Windows (WFP) отключено.*

## <a name="impact"></a>**Влияние**
*Некоторые сторонние расширения виртуального коммутатора могут работать неправильно на следующих виртуальных коммутаторах:*

\<list of virtual machines>

## <a name="resolution"></a>**Способы устранения:**
*Используйте командлет Windows PowerShell Enable-Вмсвитчекстенсион, чтобы включить платформу фильтрации Windows, если она необходима для расширений сторонних производителей.*

### <a name="enable-the-windows-filtering-platform-using-windows-powershell"></a>Включение платформы фильтрации Windows с помощью Windows PowerShell

1.  Откройте Windows PowerShell. (На рабочем столе нажмите кнопку **Пуск** и начните вводить **Windows PowerShell**.)

2.  Щелкните правой кнопкой мыши **Windows PowerShell** и выберите команду **Запуск от имени администратора**.

3.  Выполните эту команду после замены External на имя внешнего коммутатора:

```
Enable-VMSwitchExtension -VMSwitchName External -Name Microsoft Windows Filtering Platform
```

## <a name="see-also"></a>См. также:
[Enable-Вмсвитчекстенсион](https://technet.microsoft.com/library/hh848541.aspx)



