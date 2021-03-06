---
title: Настройте гостевые операционные системы для резервного копирования на основе VSS, чтобы включить моментальные снимки с единообразным использованием приложений для реплики Hyper-V.
description: Узнайте, что делать, если для моментальных снимков, совместимых с приложениями, требуется, чтобы службы теневого копирования томов (VSS) были включены и настроены в гостевых операционных системах виртуальных машин, участвующих в репликации.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
ms.date: 8/16/2016
ms.openlocfilehash: ca6b2656554f0f22a956159c770f24ad824462c6
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846081"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>Настройте гостевые операционные системы для резервного копирования на основе VSS, чтобы включить моментальные снимки с единообразным использованием приложений для реплики Hyper-V.

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Запуск сканирования анализатором соответствия рекомендациям и управление результатами сканирования](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Свойство|Сведения|
|-|-|
|**Операционная система**|Windows Server 2016|
|**Продукт или компонент**|Hyper-V|
|**Уровень серьезности**|Ошибка|
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>Проблема
*Для создания моментальных снимков, совместимых с приложениями, требуется, чтобы службы теневого копирования томов (VSS) были включены и настроились в операционных системах на виртуальных машинах, участвующих в репликации.*

## <a name="impact"></a>Влияние
*Даже если в конфигурации репликации указаны моментальные снимки с постоянными приложениями, Hyper-V не будет использовать их, если не настроена служба VSS. Это влияет на следующие виртуальные машины:*

\<list of virtual machines>

## <a name="resolution"></a>Решение
*Используйте подключение к виртуальной машине, чтобы установить службы Integration Services на виртуальной машине.*



