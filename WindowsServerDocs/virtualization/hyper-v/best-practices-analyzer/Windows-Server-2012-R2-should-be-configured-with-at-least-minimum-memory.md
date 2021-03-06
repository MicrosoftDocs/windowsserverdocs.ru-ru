---
title: Для Windows Server 2012 R2 следует настроить по крайней мере минимальный объем памяти.
description: Узнайте, что делать, если для виртуальной машины под Windows Server 2012 R2 настроено меньше минимального объема ОЗУ (512 МБ).
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 01da6f02-1a5f-4d3e-9bef-4d122a91c5c2
ms.date: 8/16/2016
ms.openlocfilehash: bd79a4804aa5d2ec9f560a0902dcfa8d468f489a
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2020
ms.locfileid: "97833669"
---
# <a name="windows-server-2012-r2-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>Для Windows Server 2012 R2 следует настроить по крайней мере минимальный объем памяти.

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство|Сведения|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Ошибка|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>**Проблема**
*Для виртуальной машины под Windows Server 2012 R2 настраивается меньше минимального объема ОЗУ, что составляет 512 МБ.*

## <a name="impact"></a>**Влияние**
*Гостевая операционная система на следующих виртуальных машинах может не запускаться или может работать ненадежно:*

\<list of virtual machines>

## <a name="resolution"></a>**Решение**
*Используйте диспетчер Hyper-V, чтобы увеличить объем памяти, выделенной для этой виртуальной машины, по крайней мере 512 МБ.*

### <a name="increase-the-memory-using-hyper-v-manager"></a>Увеличение объема памяти с помощью диспетчера Hyper-V

1.  Откройте диспетчер Hyper-V. Нажмите кнопку **Пуск**, выберите пункт **Администрирование** и затем — **Диспетчер Hyper-V**.

2.  В области результатов в разделе **виртуальные машины** выберите виртуальную машину, которую требуется настроить. Состояние виртуальной машины должно быть указано в состоянии **Off**. Если это не так, щелкните правой кнопкой мыши виртуальную машину и выберите пункт **Завершение работы**.

3.  На панели **Действия** откройте раздел **Параметры** рядом с именем виртуальной машины.

4.  В области навигации щелкните **память**.

5.  На странице **память** задайте для параметра **ОЗУ для запуска** значение не менее 512 МБ и нажмите кнопку **ОК**.

### <a name="increase-the-memory-using-windows-powershell"></a>Увеличение объема памяти с помощью Windows PowerShell

1.  Откройте Windows PowerShell. (На рабочем столе нажмите кнопку **Пуск** и начните вводить **Windows PowerShell**.)

2.  Щелкните правой кнопкой мыши **Windows PowerShell** и выберите команду **Запуск от имени администратора**.

3.  Выполните эту команду после замены на \<MyVM> имя виртуальной машины:

```
Set-VMMemory <MyVM> -StartupBytes 512MB
```

## <a name="see-also"></a>См. также:
[Set-Вммемори](/powershell/module/hyper-v/set-vmmemory)
