---
title: Основные сведения о расширениях Windows Admin Center
description: Основные сведения о расширениях SDK Windows Admin Center (проект Honolulu)
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2bcbb154c383a6683666243f6fd34ebd7124f2e8
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830639"
---
# <a name="understanding-windows-admin-center-extensions"></a>Основные сведения о расширениях Windows Admin Center

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

Если вы еще не знакомы с работой центра администрирования Windows, давайте начнем с высокоуровневой архитектуры. Windows Admin Center состоит из двух основных компонентов:

- Упрощенная **веб-служба**, которая предоставляет веб-страницы с пользовательским интерфейсом Windows Admin Center в ответ на запросы браузера.
- **Шлюзовой компонент**, который принимает запросы API-интерфейса REST от веб-страниц и ретранслирует вызовы WMI и скрипты PowerShell для выполнения на целевом сервере или в кластере.

![Схема архитектуры центра администрирования Windows.](../media/understand-extensions/wac-architecture-500px.png)

Веб-страницы с пользовательским интерфейсом Windows Admin Center, предоставляемые веб-службой, состоят из двух основных компонентов пользовательского интерфейса с точки зрения расширяемости — решений и средств, реализованных как расширения, а также расширением третьего типа, называемым подключаемыми модулями шлюза.

## <a name="solution-extensions"></a>Расширения решения

На начальном экране центра администрирования Windows по умолчанию можно добавлять подключения одного из четырех типов: подключения Windows Server, подключения к КОМПЬЮТЕРам Windows, кластеры серверов и подключения к виртуальным машинам Azure. После добавления подключения имя и тип подключения будут отображаться на главной странице. При нажатии имени подключения производится попытка подключения к целевому серверу или кластеру и последующая загрузка пользовательского интерфейса для этого подключения.

![Снимок экрана: функция добавления подключений в центре администрирования Windows.](../media/launch/use-get-started-5.png)

Каждый из этих типов подключения сопоставляется с решением, а решения определяются с помощью типа расширения, называемого расширением «решения». Решения обычно определяют уникальный тип объекта, которым вы хотите управлять через Windows Admin Center, например серверы, ПК или отказоустойчивые кластеры. Можно также определить новое решение для подключения и управления другими устройствами, например сетевыми коммутаторами и Linux-серверами или даже службами, такими как службы удаленных рабочих столов.

## <a name="tool-extensions"></a>Расширения средства

При нажатии на подключение на главной странице Windows Admin Center и подключении загружается расширение решения для выбранного типа подключения, и отображается пользовательский интерфейс решения, включая список средств в левой панели навигации. При нажатии на средство загружается пользовательский интерфейс этого средства, и он отображается в правой панели.

![Архитектура пользовательского интерфейса Windows Admin Center](../media/understand-extensions/extend-understanding-extensions-2.png)

Каждое из этих средств определяется через второй тип расширения, называемый расширением «средства». После загрузки средства оно может выполнять вызовы WMI и скрипты PowerShell на целевом сервере или в кластере и отображать информацию в пользовательском интерфейсе или выполнять команды на основании введенных пользователем данных. Расширение средства определяет, для каких решений оно должно отображаться, что обуславливает различие наборов средств для разных решений. При создании нового расширения решения вам дополнительно потребуется написать одно или несколько расширений средства, предоставляющих функциональные возможности для решения.

![Список средств для каждого решения](../media/understand-extensions/extend-understanding-extensions-3.png)

## <a name="gateway-plugins"></a>Подключаемые модули шлюза

Служба шлюза предоставляет API-интерфейсы REST для вызовов из пользовательского интерфейса и ретранслирует команды и скрипты для выполнения в целевой системе. Службу шлюза можно расширить с помощью подключаемых модулей шлюза, поддерживающих различные протоколы. Windows Admin Center предварительно оснащается двумя подключаемыми модулями шлюза; один предназначен для выполнения скриптов PowerShell, а другой — для команд WMI. Если вам потребуется взаимодействовать с целевой системой по протоколу, отличному от PowerShell и WMI, например REST, вы можете создать предназначенный для этого подключаемый модуль шлюза.

## <a name="next-steps"></a>Дальнейшие действия

В зависимости от того, какие возможности необходимо создать в Windows Admin Center, достаточным может оказаться [создание расширения средства](develop-tool.md) для существующего серверного или кластерного решения, и это самый простой первый шаг в создании расширений. Тем не менее, если ваш компонент предназначен для управления устройством, службой или чем-то совершенно новым, не сервером и не кластером, рассмотрите возможность [создания расширения решения](develop-solution.md) с помощью одного или нескольких средств. И, наконец, если необходимо взаимодействовать с целевым объектом с помощью протокола, отличного от WMI или PowerShell, необходимо [создать подключаемый модуль шлюза](develop-gateway-plugin.md). [Продолжите чтение сведений](developing-extensions.md)о том, как настроить среду разработки и начать создание первого расширения.
