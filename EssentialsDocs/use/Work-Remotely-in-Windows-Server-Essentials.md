---
title: Удаленная работа в Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 8b183f8f-1279-4fdf-a495-c7c801563cb0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 955b7e028b774699bc5170bda1fac29b88a35483
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624851"
---
# <a name="work-remotely-in-windows-server-essentials"></a>Удаленная работа в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Существует несколько способов осуществления доступа к размещенным на сервере ресурсам, если на этом сервере настроены функции повсеместного доступа (удаленный веб-доступ, частная виртуальная сеть и DirectAccess), а пользователь находится вдали от сети.

 Следующие разделы посвящены удаленному доступу к ресурсам сервера.


-   [Использование удаленного веб-доступа в Windows Server Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMA_RWA)

-   [Использование виртуальной частной сети для подключения к Windows Server Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_3)

-   [Подключение к Windows Server Essentials с помощью моего серверного приложения](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_App)

-   [Использование приложения "Мой сервер" для Windows Phone](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)

-   [Использование Microsoft 365 с Windows Server Essentials](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_O365)

> [!NOTE]
>  Сведения о настройке повсеместного доступа на сервере см. в разделе [Управление повсеместным доступом](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md).

##  <a name="use-remote-web-access-in-windows-server-essentials"></a><a name="BKMA_RWA"></a> Использование удаленного Веб-доступ в Windows Server Essentials

 Удаленный веб-доступ позволяет сохранять подключение к сети Windows Server Essentials, находясь за пределами офиса. Дополнительные сведения см. в разделе [Использование удаленного веб-доступ](Use-Remote-Web-Access-in-Windows-Server-Essentials.md).


##  <a name="use-vpn-to-connect-to-windows-server-essentials"></a><a name="BKMK_3"></a> Использование VPN для подключения к Windows Server Essentials
 При наличии клиентского компьютера, на котором настроены сетевые учетные записи, которые можно использовать для подключения к размещенному серверу, работающему под управлением Windows Server Essentials через VPN-подключение, все вновь создаваемые пользовательские учетные записи на размещенном сервере должны использовать для первого входа на клиентский компьютер VPN-подключение. Выполните следующие действия с клиентского компьютера, подключенного к серверу.

#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>Использование виртуальной частной сети для удаленного доступа к серверным ресурсам

1.  На клиентском компьютере нажмите клавиши CTRL+ALT+DELETE.

2.  На экране входа в систему щелкните **Сменить пользователя**.

3.  Щелкните значок входа в сеть в нижнем правом углу экрана.

4.  Выполните вход в сеть Windows Server Essentials, указав сетевые имя пользователя и пароль.

##  <a name="use-the-my-server-app-to-connect-to-windows-server-essentials"></a><a name="BKMK_App"></a> Подключение к Windows Server Essentials с помощью моего серверного приложения
 Мое серверное приложение позволяет подключаться к ресурсам и выполнять облегченные задачи администрирования на сервере Windows Server Essentials с компьютера под управлением Windows, ноутбука или Surface Device. Если сервер работает под Windows Server 2012, скачайте исходное серверное приложение из [приложений для Windows](https://windows.microsoft.com/windows-8/apps). Если сервер работает под Windows Server Essentials, вместо него необходимо загрузить приложение сервера 2012 R2.

 С расширенным приложением My Server 2012 R2 можно подключаться к серверным или клиентским компьютерам с использованием удаленного рабочего стола. Если сервер Windows Server Essentials интегрирован с Microsoft 365, а подписка включает SharePoint Online, вы также можете работать с документами в библиотеках SharePoint Online и открывать сайты групп SharePoint с сервера 2012 R2.


 Сведения об установке и использовании этих приложений см. [в разделе Использование приложения My Server](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).

 Сведения об установке и использовании этих приложений см. [в разделе Использование приложения My Server](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md).


##  <a name="use-the-my-server-app-for-windows-phone"></a><a name="BKMK_2"></a> Использование серверного приложения для Windows Phone
 Приложение моего сервера Windows для Windows Phone (для Windows Server 2012) и приложение My Server 2012 R2 для Windows Phone (для Windows Server Essentials) предназначены для обеспечения беспрепятственного подключения к серверам через смарт-телефоны при работе в удаленных точках. Это один из различных способов доступа к Windows Server Essentials после настройки сервера для удаленного доступа.

 Можно загрузить любое из нижеперечисленных приложений из Магазина Windows Phone:

- [Установка приложения My Server для Windows Phone.](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)

- [Установка приложения My Server 2012 R2 для Windows Phone](http://www.windowsphone.com/store/app/my-server-2012-r2/44f596b5-0477-4096-b96e-ddd6ef64ad6b)

  Дополнительные сведения о приложении "мой сервер Phone" см. в записи блога [мое приложение Server Phone для Windows Server Essentials](/archive/blogs/sbs/my-server-phone-app-for-windows-server-2012-essentials). Сведения о приложении My Server 2012 R2 для телефона см. в записи блога [Приложения My Server 2012 R2 для Windows и Windows Phone](/archive/blogs/sbs/my-server-2012-r2-windows-and-windows-phone-apps).

##  <a name="use-microsoft-365-with-windows-server-essentials"></a><a name="BKMK_O365"></a> Использование Microsoft 365 с Windows Server Essentials

 Microsoft 365 — это простой в использовании набор средств с поддержкой веб-служб, позволяющих получать доступ к электронной почте, важным документам, контактам и календарям практически из любого места и с любого устройства. Дополнительные сведения см. в [Краткое руководство по началу работы с использованием Microsoft 365](Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).


## <a name="see-also"></a>См. также раздел

-   [Управление повсеместным доступом](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Подключиться](Get-Connected-in-Windows-Server-Essentials.md)

-   [Использование общих папок](Use-Shared-Folders-in-Windows-Server-Essentials.md)

-   [Воспроизведение цифрового мультимедиа](Play-Digital-Media-in-Windows-Server-Essentials.md)