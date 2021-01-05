---
title: Управление SharePoint Online в Windows Server Essentials
description: Узнайте, как управлять библиотеками и сайтами групп SharePoint Online с панели мониторинга без входа в Microsoft 365.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 282f3634-6de6-4691-803c-df6c3c16660d
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 5d7e7e033cbaa625bf9865822cc12f290136e791
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97811251"
---
# <a name="manage-sharepoint-online-in-windows-server-essentials"></a>Управление SharePoint Online в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Вы можете управлять библиотеками и сайтами групп SharePoint Online с панели мониторинга, не входя в Microsoft 365, если вы интегрируете Microsoft 365 с сервером Windows Server Essentials. Вы получаете библиотеки SharePoint Online и сайты рабочих групп с любым Microsoft 365 бизнес-планом. [Узнайте, как интегрировать Microsoft 365 с сервером](Manage-Office-365-in-Windows-Server-Essentials.md)

 В качестве премии пользователи смогут использовать приложение "мой сервер 2012 R2" для доступа к файлам в библиотеках SharePoint Online из любого места с помощью мобильного устройства или Windows Phone. [Где найти приложение "Мой сервер"?](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)

 Еще не пробовали SharePoint? [Действия](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)

## <a name="where-on-the-dashboard-will-i-manage-my-libraries-and-team-sites"></a>Где на панели мониторинга находится управление библиотеками и сайтами групп?
 Вы будете использовать новую вкладку **SharePoint Online** , которая добавляется в область **хранения** панели мониторинга при интеграции Microsoft 365 с сервером, для управления ресурсами SharePoint Online.


## <a name="what-can-i-manage-from-the-dashboard"></a>Чем можно управлять с помощью панели мониторинга?

### <a name="manage-your-online-libraries"></a>Управление интерактивными библиотеками

- **Добавьте библиотеку.** На вкладке **Библиотеки SharePoint** нажмите **Добавить библиотеку**. Вы сможете настроить следующие стандартные параметры:
  - Выбор сайта группы и типа библиотеки.
  - Использование управления версиями.
  - Определение прав доступа.
     **Совет.** Чтобы узнать, какие разрешения сайта группы будут наследоваться библиотекой, если вы не назначите разрешения, используйте **параметр Просмотреть разрешения сайта**.
- **Откройте библиотеку.** Для работы с содержимым библиотеки необходимо открыть ее в Microsoft 365. Выберите библиотеку и нажмите **Открыть библиотеку**. То, что можно делать с содержимым, зависит от учетных данных, используемых для входа в SharePoint Online.
- **Изменение элементов управления версиями или разрешений на доступ.** С помощью раздела **Параметры библиотеки** можно просматривать и редактировать параметры версии и права доступа к библиотеке.
- **Удаление библиотеки.** После того, как вы убедитесь, что сохранили все необходимые данные, выберите библиотеку и нажмите **Удалить библиотеку**. **Предупреждение:** Перед удалением библиотеки SharePoint Online не забудьте сохранить все файлы, которые необходимо сохранить в другом расположении. При удалении библиотеки из SharePoint все удаляются без возможности восстановления. Восстановление невозможно.

### <a name="manage-your-team-sites"></a>Управление сайтами группы

- **Управление сайтами групп SharePoint.** Действие **Manage Team Sites (Управление сайтами группы** ) позволяет входить в Microsoft 365 и управлять сайтами групп SharePoint Online. Действия, которые можно выполнить в Microsoft 365, определяются учетной записью, используемой для входа в Интернет. Когда вы закроете Microsoft 365 и вернетесь на панель мониторинга, нажмите кнопку **Обновить** , чтобы отобразить изменения.
- **Просмотр или изменение разрешений для сайта рабочей группы.** Поскольку библиотека наследует разрешения от своего сайта группы по умолчанию, полезно иметь простой доступ к сайту группы. Чтобы просмотреть или изменить разрешения для сайта группы, выберите сайт группы или любую из его библиотек и щелкните **просмотреть разрешения сайта**. **Совет.** Нужна помощь с тонкими точками разрешений для сайта группы SharePoint? Воспользуйтесь полезной ссылкой [Подробнее](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924) на странице разрешений сайта группы.

## <a name="tips"></a>Советы

-   **Нажмите кнопку обновить, чтобы отобразить последние изменения, внесенные на портале Microsoft 365.** После открытия Microsoft 365 для управления SharePoint Online необходимо обновить экран. Если панель мониторинга длительные периоды времени остается открытой, нажимайте **Обновить** для отображения последних изменений.

-   **Действия, которые можно выполнять в SharePoint Online, зависят от того, работаете ли вы на панели мониторинга или в Microsoft 365.** На панели мониторинга изменения SharePoint Online выполняются с использованием учетной записи администратора для интеграции Microsoft 365. Но при входе в Microsoft 365 с панели мониторинга разрешения на доступ к учетной записи Online, которую вы используете, определяют, что вы можете делать.

     Чтобы узнать учетную запись администратора для Microsoft 365ной интеграции, откройте вкладку **Microsoft 365** на панели мониторинга.

## <a name="other-things-you-might-want-to-do"></a>Дополнительные сведения

-   [Использование приложения "Мой сервер" для работы с библиотеками SharePoint Online, где бы вы ни находились](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)

-   [Дополнительные сведения о назначении разрешений для сайтов групп SharePoint](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924)

-   [Действия, которые можно выполнять с помощью функций SharePoint](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)

-   [Взгляните на Microsoft 365 доступные бизнес-планы](https://office.microsoft.com/business/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_what-is-office-365-for_Text)

-   [Интеграция Microsoft 365 с сервером](Manage-Office-365-in-Windows-Server-Essentials.md)

-   [Управление другими онлайн-службами Майкрософт при помощи панели мониторинга](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
