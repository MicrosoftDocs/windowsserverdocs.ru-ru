---
title: Шаг 3. Присоединение компьютеров к новому серверу Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0e07d1a-8409-429b-87d7-0f4a7e14d668
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ca1e3a031c95f19fb68aadcf203b13fa39d7558
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318763"
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>Шаг 3. Присоединение компьютеров к новому серверу Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Следующим шагом процесса миграции является подключение клиентских компьютеров к новому серверу под управлением Windows Server Essentials.  
  
> [!NOTE]
>  Для компьютеров с ОС Windows XP или Windows Vista этот шаг можно пропустить. Программное обеспечение Windows Server Connector не поддерживает компьютеры, на которых выполняется ОС Windows XP или Windows Vista.  
  
 Перед присоединением клиентского компьютера к новому серверу Windows Server Essentials необходимо отключить его от исходного сервера, отменив установку программного обеспечения соединителя Windows Server на клиентском компьютере.  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>Удаление Windows Server Connector на клиентском компьютере  
  
1.  На клиентском компьютере откройте панель управления, а затем **Программы и компоненты**.  
  
2.  В списке программ щелкните правой кнопкой мыши приложение Connector, выполняемое на вашем компьютере.  
  
    > [!NOTE]
    >  Приложение соединителя может быть **соединителем Windows Small Business Server 2011 Essentials**или **соединителем Windows Server Essentials**в зависимости от версии Windows Server Essentials, к которой подключен клиентский компьютер.  
  
3.  Щелкните **Удалить**.  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>Повторное подключение клиентского компьютера к серверу  
  
1.  Войдите на компьютер, который требуется подключить к серверу.  
  
    > [!NOTE]
    >  Если на компьютере настроено несколько учетных записей пользователей, войдите в систему с той учетной записью, документы, изображения и личные настройки которой требуется сохранить после подключения этого компьютера к серверу.  
  
2.  Откройте браузер, например Internet Explorer.  
  
3.  В адресной строке введите **http://< servername\>/Коннект**и нажмите клавишу ВВОД.  
  
4.  Следуйте инструкциям на экране, чтобы присоединить клиентский компьютер к новому серверу Windows Server Essentials.  
  
## <a name="next-steps"></a>Следующие шаги  
 Вы присоединяете клиентские компьютеры к новому серверу под управлением Windows Server Essentials. Теперь перейдите к [шагу 4. Перемещение параметров и данных на целевой сервер для миграции Windows Server Essentials](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  
  

Для просмотра всех шагов см. статью [Переход на Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

