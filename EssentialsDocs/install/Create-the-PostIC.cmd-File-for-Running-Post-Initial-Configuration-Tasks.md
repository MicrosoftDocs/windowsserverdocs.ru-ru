---
title: Создание файла PostIC.cmd для выполнения задач после завершения начальной настройки
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 99e258bc-0695-48c9-b694-a7f3cbe2a2d0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 5a3ae6711d54d1c1f2bebdae6db3065fce970312
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623712"
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>Создание файла PostIC.cmd для выполнения задач после завершения начальной настройки

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Существует возможность добавления настройки после начальной конфигурации; для этого необходимо написать собственный код, и затем вызвать этот код из файла сценария под именем PostIC.cmd. При использовании файла PostIC.cmd необходимо соблюдать следующие правила:

- Код настройки должен выполняться без вмешательства пользователя (он не может отображать пользовательский интерфейс).

- Код настройки не может инициировать перезагрузку сервера. Перезагрузка сервера будет произведена в качестве последней задачи начальной настройки.

- Выполнение кода настройки должно продолжаться не более трех минут.

  Необходимо определить файл PostIC.cmd таким образом, чтобы в случае успешного выполнения кода возвращалось значение 0. При возвращении другого значения операционной системой выполняется поиск файла [SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure), содержащего код, который должен выполняться в случае неудачного завершения скрипта PostIC.cmd. Файлы PostIC.cmd и SetupFailure.cmd должны быть расположены в папке C:\Windows\Setup\Scripts.

#### <a name="to-define-post-initial-configuration-customizations"></a>Определение настроек, выполняемых после начальной настройки

1.  Напишите код, вызываемый из скрипта PostIC.cmd.

2.  С помощью Блокнота создайте файл с именем PostIC.cmd и добавьте в него вызов кода, написанного на шаге 1. Убедитесь, что код возвращает значение успешного выполнения.

3.  Сохраните файл PostIC.cmd в папке C:\Windows\Setup\Scripts.

4.  (Необязательно) Создайте файл SetupFailure.cmd, содержащий код, который выполняется, если файл PostIC.cmd возвращает значение, отличное от 0.

###  <a name="setupfailurecmd"></a><a name="BKMK_SetupFailure"></a> Сетупфаилуре. cmd
 С помощью SetupFailure.cmd можно активировать отправку уведомлений о проблемах в начальной настройке. Файл SetupFailure.cmd содержит код, который следует запускать в случае возникновения проблемы. Файл SetupFailure.cmd расположен в папке C:\Windows\Setup\Scripts; он запускается при возникновении проблемы с задачей установки или при возвращении файлом PostIC.cmd значения, отличного от 0.

##### <a name="to-define-notifications"></a>Определение уведомлений

1.  Напишите код, вызываемый из скрипта SetupFailure.cmd.

2.  С помощью Блокнота создайте файл с именем SetupFailure.cmd и добавьте в него вызов кода, написанного на шаге 1. Убедитесь, что код возвращает значение успешного выполнения.

3.  Сохраните файл SetupFailure.cmd в папке C:\Windows\Setup\Scripts.

## <a name="see-also"></a>См. также:
 [Начало работы с Windows Server ESSENTIALS ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)