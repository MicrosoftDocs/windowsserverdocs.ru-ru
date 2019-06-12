---
title: Установка и настройка Windows Server Essentials или режима Windows Server Essentials
description: Описывает способ использования Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f5593c21b99f4f8cb22979d5dc201a38e54be84c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433487"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Установка и настройка Windows Server Essentials или режима Windows Server Essentials

>Область применения. Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials — это оптимальный сервер для малого бизнеса с максимум 25 пользователей и 50 устройств. Для организаций с до 100 пользователей и 200 устройств теперь можно использовать Windows Server 2012 R2 с установленной ролью Windows Server Essentials Experience. В данном разделе рассматриваются оба варианта.  
  
Windows Server Essentials Experience — это роль в Windows Server 2016, которая позволяет воспользоваться преимуществами всех функций (например, удаленного веб-доступа и резервного Копирования), доступные в Windows Server Essentials без блокировок и ограничений, которые применяются в  Windows Server Essentials. Эта роль сервера также доступна в Windows Server Essentials и включена по умолчанию.
  
Перед установкой Windows Server Essentials или роль Essentials Experience следует помнить о следующих ограничениях.  
  
|Windows Server Essentials Experience в Windows Server Essentials|Windows Server Essentials Experience в Windows Server 2016
|----|----|
|— Должен быть контроллером домена в корне леса и домена и выполнять все роли FSMO.<br /><br /> — Не может устанавливаться в среде с существующим доменом Active Directory (тем не менее, есть льготный период длительностью 21 день для осуществления миграции).|-Нет должен быть контроллером домена, если он установлен в среде с существующим доменом Active Directory.<br /><br /> — Если существует домен Active Directory, Установка роли создаст домен Active Directory, и сервер станет контроллером домена в корне леса и домена, содержащий все роли FSMO.  
|Развертывание возможно только в одном домене.|Развертывание возможно только в одном домене.  
|Контроллер домена только с правами чтения не может существовать в вашем домене.|Контроллер домена только с правами чтения не может существовать в вашем домене.

> [!NOTE]
>  Для загрузки ознакомительных версий этих операционных систем посетите Центр пробного ПО TechNet:  
>   
>  [Скачайте Windows Server 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Скачивание Windows Server Essentials](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>Параметры установки  
 Этот документ содержит пошаговые инструкции по установке и настройке Windows Server Essentials. В зависимости от сетевой среды имеются следующие доступные параметры установки:  
  
-    Windows Server Essentials (с ролью Windows Server Essentials Experience включен по умолчанию)  
  
-    Windows Server 2016 с установленной ролью Windows Server Essentials Experience  
 
|Среда развертывания|Описание|См. также|  
|----------------------------|-----------------|---------------------|  
|Новая среда Active Directory|Для создания новой среды Active Directory можно установить Windows Server Essentials.|[Развертывание Windows Server Essentials для настройки новой среды Active Directory](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|Существующая среда Active Directory|Можно установить Windows Server Essentials в существующую среду Active Directory.|[Развертывание Windows Server Essentials в существующей среде Active Directory](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|Виртуальная среда|Можно развернуть Windows Server Essentials в качестве виртуальной машины.|[Создать виртуальную среду](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|Автоматическое развертывание|Автоматизация развертывания Windows Server Essentials с помощью Windows PowerShell.|[Установка и настройка Windows Server Essentials с помощью Windows PowerShell](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>Перед началом работы  
 Перед началом установки необходимо ознакомиться со следующей документацией:  
  
-   [Обзор продукта Windows Server Essentials](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Системные требования к Windows Server Essentials](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a> Развертывание Windows Server Essentials для настройки новой среды Active Directory  
 Windows Server Essentials позволяет быстро настроить среду Active Directory и соответствующие серверные функции.  
  
###  <a name="BKMK_WSEDeploy"></a> Развертывание Windows Server Essentials  
 Если вы используете Windows Server Essentials, Windows Server Essentials Experience уже включен. Тем не менее, необходимо выполнить некоторые действия для настройки сервера.  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>Чтобы настроить Windows Server Essentials на физическом сервере  
  
1. После страницы **приветствия** на рабочем столе появляется **Мастер настройки Windows Server Essentials**.  
  
2. Для завершения работы мастера настройки следуйте инструкциям ниже:  
  
   1.  На странице **Настройка Windows Server Essentials** нажмите кнопку **Далее**.  
  
   2.  На странице **Параметры времени**проверьте правильность указанной даты, времени и часового пояса и нажмите кнопку **Далее**.  
  
   3.  На странице **Сведения о компании** введите название вашей компании, например **Contoso,Ltd.** , и нажмите кнопку **Далее**. При необходимости можно изменить внутреннее имя домена и имя сервера.  
  
   4.  На странице **Создание учетной записи администратора сети**введите новое имя и пароль учетной записи администратора.  
  
       > [!NOTE]
       >  Не используйте имя и пароль учетной записи **Администратора** по умолчанию.  
  
   5.  Щелкните **Настройка**.  
  
3. В процессе настройки сервер несколько раз перезагрузится, при этом вход в систему будет производиться автоматически до завершения настройки. Этот процесс занимает примерно 20 минут.  
  
4. На рабочем столе щелкните значок панели мониторинга для запуска панели мониторинга. На **домашней** странице выполните задачи **Приступая к работе**, перечисленные на вкладке **Установка**.  
  
   После завершения настройки сервер под управлением Windows Server Essentials будет установлен как контроллер домена.  
  
###  <a name="BKMK_DeployWSERole"></a> Развертывание роли Windows Server Essentials Experience в Windows Server 2012 R2 Standard и Datacenter  
 Для включения и настройки роли Windows Server Essentials Experience в Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter, используя следующую процедуру можно использовать диспетчер серверов.  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Развертывание роли Windows Server Essentials Experience в Windows Server 2012 R2  
  
1.  Войдите в сервер с правами локального администратора.  
  
2.  Откройте **Диспетчер сервера**, а затем щелкните **Добавить роли и компоненты**.  
  
3.  На вкладке **Выбор ролей сервера**выберите роль **Windows Server Essentials Experience** . В диалоговом окне выберите **Добавить компоненты**и нажмите кнопку **Далее**.  
  
4.  На странице **Компоненты**нажмите кнопку **Далее**.  
  
5.  Просмотрите описание роли **Windows Server Essentials Experience** и нажмите кнопку **Далее**.  
  
6.  На следующих страницах нажимайте кнопку **Далее**, а затем на странице подтверждения нажмите кнопку **Установка**.  
  
7.  После завершения установки Windows Server Essentials Experience должен быть указан как роль сервера в диспетчере сервера.  
  
8.  В области уведомлений в диспетчере сервера установите флажок, а затем выберите **Настройка Windows Server Essentials**.  
  
9. (Необязательно) При необходимости измените имя сервера.  
  
    > [!IMPORTANT]
    >  После настройки Windows Server Essentials нельзя изменить имя сервера.  
  

10. Следуйте инструкциям мастера настройки Windows Server Essentials, как описано в [развертывание Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) раздел.  

10. Следуйте инструкциям мастера настройки Windows Server Essentials, как описано в [развертывание Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) раздел.  

  
##  <a name="BKMK_ExistingAD"></a> Развертывание Windows Server Essentials в существующей среде Active Directory  
 Если в организации уже существует среда Active Directory, в ней также можно развернуть Windows Server Essentials. Кроме того, по выбору можно развернуть Windows Server Essentials в качестве контроллера домена.  
  
> [!IMPORTANT]
>  Этот параметр доступен только в том случае, если развертывание роли Windows Server Essentials Experience в Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter.  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>Развертывание Windows Server Essentials в существующей среде Active Directory  
  
1.  (Необязательно) При необходимости измените имя сервера.  
  
    > [!IMPORTANT]
    >  После настройки Windows Server Essentials нельзя изменить имя сервера.  
  
2.  Присоединение сервера под управлением Windows Server Essentials к существующему домену происходит следующим образом.  
  
    1.  Если этот сервер должен быть контроллером домена, настройте его как копию контроллера домена.  
  
    2.  Если этот сервер не должен быть контроллером домена, присоедините сервер к вашему домену с помощью собственных средств Windows.  
  
3.  Перезагрузите сервер и войдите в него как администратор домена.  
  
4.  Откройте диспетчер домена и щелкните **Добавить роли и компоненты**.  
  
5.  На последующих страницах нажимайте кнопку **Далее**.  
  
6.  На вкладке **Выбор ролей сервера**выберите **Windows Server Essentials Experience**. В диалоговом окне выберите **Добавить компоненты**и нажмите кнопку **Далее**.  
  
7.  На странице **Компоненты**нажмите кнопку **Далее**.  
  
8.  Просмотрите описание **Windows Server Essentials Experience** и нажмите кнопку **Далее**.  
  
9. На следующих страницах нажимайте кнопку **Далее**, а затем на странице подтверждения нажмите кнопку **Установка**.  
  
10. После завершения установки Windows Server Essentials Experience будет указана в качестве роли сервера в диспетчере сервера.  
  
11. В области уведомлений в **диспетчере сервера** установите флажок, а затем выберите **Настройка Windows Server Essentials**.  
  
12. Следуйте инструкциям мастера настройки Windows Server Essentials. В зависимости от конфигурации Active Directory вы получите уведомление о настройке Windows Server Essentials в качестве контроллера домена или в качестве члена домена. Щелкните **Настройка**, чтобы приступить к настройке. Процесс настройки занимает около 10 минут.  
  
##  <a name="BKMK_VirtualWSE"></a> Создать виртуальную среду  
  Windows Server Essentials, Windows Server 2012 R2 Standard и Windows Server 2012 R2 Datacenter могут выполняться как виртуальные машины. Виртуальные машины запускаются с помощью средств управления Hyper-V на сервере с Hyper-V. С точки зрения лицензирования Windows Server Essentials позволяет настроить роль Hyper-V и создать виртуальную среду. Лицензия позволяет настроить другую гостевую ОС, на котором работает Windows Server Essentials. В зависимости от поставщика системы «конфигурации s™, Windows Server Essentials позволяет легко настроить виртуальную среду.  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Развертывание Windows Server Essentials в качестве виртуальной машины.  
  
1.  После страницы приветствия Windows (в зависимости от поставщика «™ s конфигурации системы) **перед началом** страница предоставляет возможность настроить Windows Server Essentials в качестве виртуальной машины или на физическом оборудовании. Наличие данных параметров определяется поставщиком вашей системы, поэтому оба этих параметра могут быть не всегда доступны. Для установки Windows Server Essentials в качестве виртуальной машины, в **Установка Windows Server Essentials**выберите **установить как виртуальный экземпляр**, а затем нажмите кнопку **Настройка**.  
  
2.  Мастер настройки начнет приводить в действие виртуальную машину, что занимает около пяти минут.  
  

3.  Затем настройте Windows Server Essentials, как описано выше в [развертывание Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) раздел.  

3.  Затем настройте Windows Server Essentials, как описано выше в [развертывание Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) раздел.  

  
##  <a name="BKMK_PowerShell"></a> Установка и настройка Windows Server Essentials с помощью Windows PowerShell  
 С помощью командлетов Windows PowerShell можно автоматизировать установку Windows Server Essentials.  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Установка Windows Server Essentials с помощью Windows PowerShell  
  
1.  Откройте консоль Windows PowerShell из командной строки с повышенными привилегиями.  
  
2.  Установка роли Windows Server Essentials Experience с помощью следующей команды:  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  Выполните команду `Get-Help Start-WssConfigurationService`.  
  
    1.  Выполните следующую команду, чтобы начать настройку Windows Server Essentials в качестве контроллера домена:  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  Выполните следующую команду, чтобы начать настройку Windows Server Essentials в качестве члена домена. Для выполнения этой задачи необходимо быть членом группы администраторов предприятия или группы администраторов домена в Active Directory:  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  Контролируйте ход процесса установки с помощью следующих команд:  
  
    -   Для отображения хода установки с помощью индикатора выполнения выполните команду `Get-WssConfigurationStatus  œShowProgress`.  
  
    -   Для получения немедленных сведений о процессе установки без индикатора выполнения выполните команду `Get-WssConfigurationStatus`.  
  
## <a name="see-also"></a>См. также  
  
-   [Новые возможности в Windows Server Essentials](../get-started/what-s-new.md)  
  
-   [Установка Windows Server Essentials](Install-Windows-Server-Essentials.md)  
  
-   [Начало работы с Windows Server Essentials](../get-started/get-started.md)
