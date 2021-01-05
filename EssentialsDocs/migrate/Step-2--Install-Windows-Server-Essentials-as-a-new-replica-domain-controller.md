---
title: Шаг 2. Установка Windows Server Essentials в качестве нового репликата контроллера домена
description: Узнайте, как установить Windows Server Essentials и Windows Server 2012 R2 Standard (с включенной ролью Windows Server Essentials) в качестве контроллера домена.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c7ccfc34-63fd-436b-a1cd-e05810f60bfe
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 64e6cbbf3eefd34e9373dcb1e49b3626e6014368
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810551"
---
# <a name="step-2-install-windows-server-essentials-as-a-new-replica-domain-controller"></a>Шаг 2. Установка Windows Server Essentials в качестве нового репликата контроллера домена

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

В этом разделе описывается установка Windows Server Essentials и Windows Server 2012 R2 Standard (с включенной ролью Windows Server Essentials) в качестве контроллера домена.

 Для сред, в которых до 25 пользователей и устройств 50, можно выполнить действия, описанные в этом руководстве, для перехода с предыдущих версий Windows SBS на Windows Server Essentials. Для сред, в которых 100 пользователей и 200 устройств, вы можете использовать те же рекомендации для перехода на стандартные и выпуски Datacenter в Windows Server 2012 R2 с установленной ролью Windows Server Essentials Experience. В этом документе рассматриваются оба сценария.

> [!IMPORTANT]
>  При переходе на Windows Server Essentials следующее сообщение об ошибке добавляется в журнал событий каждый день в течение 21-дневного льготного периода до тех пор, пока исходный сервер не будет удален из сети. По истечении 21-дневного льготного периода работа исходного сервера завершается. <br> **Проверка роли FSMO обнаружила в вашей среде условие, которое не соответствует политике лицензирования. Сервер управления должен содержать роли основного контроллера домена и хозяина именования доменов Active Directory ролей. Перенесите роли Active Directory на сервер управления сейчас. Этот сервер будет автоматически выключен, если проблема не была исправлена в течение 21 дня с момента первого обнаружения этого условия**.

#### <a name="install-windows-server-essentials-or-windows-server-2012-r2-standard-on-the-destination-server"></a>Установка Windows Server Essentials или Windows Server 2012 R2 Standard на целевом сервере

1.  Установите Windows Server Essentials или Windows Server 2012 R2 Standard с включенной ролью Windows Server Essentials Experience, следуя инструкциям в [статье Установка и настройка Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

    > [!NOTE]
    >  Если будет запущен мастер настройки Windows Server Essentials, отмените его.

2.  Перенесите роли FSMO с исходного сервера.

    > [!NOTE]
    >  Если Windows Server Essentials является единственным контроллером домена в домене, то роль FSMO автоматически перемещается на сервер под операционной системой Windows Server Essentials при понижении уровня исходного сервера.

3.  Откройте диспетчер серверов и запустите мастер добавления ролей и компонентов.

4.  Если роль Windows Server Essentials Experience не установлена, добавьте ее.

5.  После установки роли Windows Server Essentials Experience в области уведомлений появляется задача "Настройка Windows Server Essentials". Для запуска мастера настройки Windows Server Essentials щелкните эту задачу.

6.  Следуйте инструкциям для завершения процесса настройки Windows Server Essentials. Перед запуском мастера выполните следующие действия.

    -   При необходимости, измените имя сервера, так как после завершения работы мастера настройки Essentials Windows Server изменить имя будет невозможно.

    -   Убедитесь, что время и параметры сервера указаны правильно.

7.  Проверьте установку следующим образом:

    1.  Откройте панель мониторинга.

    2.  Перейдите на вкладку **Пользователи** и убедитесь, что учетные записи пользователей указаны в Active Directory.

### <a name="transfer-the-operations-master-roles"></a>Перенос ролей хозяина операций
 Хозяин операций (также называемый гибкими одиночными главными операциями или FSMO) должен быть передан с исходного сервера на целевой сервер в течение 21 дня после установки Windows Server Essentials на целевом сервере.

##### <a name="to-transfer-the-operations-master-roles"></a>Перенос ролей хозяина операций

1.  На целевом сервере откройте окно командной строки от имени администратора. См. раздел [Открытие окна командной строки от имени администратора](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx).

2.  В командной строке введите **NETDOM QUERY FSMO** и нажмите клавишу "ВВОД".

3.  В командной строке введите **ntdsutil** и нажмите клавишу "ВВОД".

4.  В командной строке  **ntdsutil** введите следующие команды:

    1.  Введите **activate instance NTDS** и нажмите клавишу ВВОД.

    2.  Введите **roles** и нажмите клавишу "ВВОД".

    3.  Введите **connections** и нажмите клавишу "ВВОД".

    4.  Введите **Подключение к серверу** *<ServerName \>* (где *<ServerName \>* — имя целевого сервера) и нажмите клавишу ВВОД.

    5.  В окне командной строки введите **q** и нажмите клавишу "ВВОД".

        1.  Введите **transfer PDC**, нажмите клавишу ВВОД и щелкните **Да** в диалоговом окне **Подтверждение передачи роли**.

        2.  Введите **transfer infrastructure master**, нажмите клавишу "ВВОД" и щелкните **Да** в диалоговом окне **Подтверждение передачи роли**.

        3.  Введите **transfer naming master**, нажмите клавишу "ВВОД" и щелкните **Да** в диалоговом окне **Подтверждение передачи роли**.

        4.  Введите **transfer RID master**, нажмите клавишу "ВВОД" и щелкните **Да** в диалоговом окне **Подтверждение передачи роли**.

        5.  Введите **transfer schema master**, нажмите клавишу "ВВОД" и щелкните **Да** в диалоговом окне **Подтверждение передачи роли**.

    6.  Введите **q** и нажимайте клавишу ВВОД до тех пор, пока не вернетесь в командную строку.

> [!NOTE]
>  На любом сервере в сети вы можете убедиться, что роли хозяина операций были перенесены на кольцевой сервер. Откройте окно командной строки от имени администратора (дополнительные сведения см. в разделе [Открыть окно командной строки от имени администратора](https://technet.microsoft.com/library/cc947813\(v=WS.10\).aspx)). Введите **netdom query fsmo** и нажмите клавишу "ВВОД".

## <a name="next-steps"></a>Дальнейшие действия
 Вы установили Windows Server Essentials как новый контроллер домена реплики. Теперь перейдите к разделу [Шаг 3. Присоединение компьютеров к новому серверу Windows Server Essentials](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md).

Для просмотра всех шагов см. статью [Переход на Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

