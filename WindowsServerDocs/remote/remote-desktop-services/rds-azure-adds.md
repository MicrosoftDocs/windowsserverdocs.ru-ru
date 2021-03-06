---
title: Доменные службы Azure AD и службы удаленных рабочих столов
description: Узнайте, как интегрировать доменные службы Azure AD в среду развертываемых служб удаленных рабочих столов.
ms.author: chrimo
ms.date: 10/02/2017
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: 57d9212c9a3156ead8c17b86ca78b4965c020bf3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961848"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>Интеграция доменных служб Azure AD в среду развертываемых служб удаленных рабочих столов

Используйте [доменные службы Azure AD](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS) в развертывании служб удаленных рабочих столов вместо Windows Server Active Directory. Доменные службы Azure AD позволяют использовать существующие удостоверения Azure AD в классических рабочих нагрузках Windows.

С помощью доменных служб Azure AD можно:
- создать среду Azure с локальным доменом для полностью облачных организаций;
- создать изолированную среду Azure с теми же удостоверениями, которые используются для локальной и онлайн-среды без необходимости создания соединения ExpressRoute или VPN-соединения типа "сеть-сеть".

Когда интеграция доменных служб Azure AD со службой удаленных рабочих столов завершится, архитектура будет иметь следующий вид.

![Схема архитектуры служб удаленных рабочих столов с доменными службами Azure AD](media/aadds-rds.png)

Чтобы сравнить эту архитектуру с другими сценариями развертывания служб удаленных рабочих столов, см. статью [Архитектура служб удаленных рабочих столов](desktop-hosting-logical-architecture.md).

Чтобы лучше понять доменные службы Azure AD, ознакомьтесь со статьями [Обзор доменных служб Azure AD](/azure/active-directory-domain-services/active-directory-ds-overview) и [Как определить, подходит ли доменные службы Azure AD для вашего варианта использования](/azure/active-directory-domain-services/active-directory-ds-comparison).

Используйте следующие сведения для использования доменных служб Azure AD со службой удаленных рабочих столов.

## <a name="prerequisites"></a>Предварительные условия

Прежде чем использовать удостоверения из Azure AD для развертывания служб удаленных рабочих столов, [настройте Azure AD для сохранения хэшированных паролей для удостоверений пользователей](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync). Облачные организации не требуют внесения никаких дополнительных изменений в каталог. Тем не менее, локальные организации должны разрешить синхронизацию и сохранение хэшированных паролей в доменных службах Azure, что приемлемо не для всех организаций. Пользователи вынуждены сбрасывать свои пароли после смены настроек.

## <a name="deploy-azure-ad-ds-and-rds"></a>Развертывание доменных служб Azure AD и служб удаленных рабочих столов
Выполните следующие действия для развертывания доменных служб Azure AD и служб удаленных рабочих столов.

1. Включите [доменные службы Azure AD](/azure/active-directory-domain-services/active-directory-ds-getting-started). Обратите внимание, что статья по ссылке охватывает следующие действия:
   - создание соответствующих групп доменных служб Azure для управления доменом;
   - определение момента, когда пользователям необходима смена пароля, чтобы их учетные записи могли работать с доменными службами Azure AD.

2. Задайте настройки службы удаленных рабочих столов. Вы можете использовать шаблон Azure или развернуть службу удаленных рабочих столов вручную.
   - Используйте [существующий шаблон доменных служб](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/). Не забудьте задать следующие настройки.

     - **Параметры**
       - **Группа ресурсов** Используйте группу ресурсов, в которой вы хотите создать ресурсы служб удаленных рабочих столов.
         > [!NOTE]
         > Это должна быть та же группа ресурсов, в которой существует виртуальная сеть диспетчера ресурсов Azure.

       - **Префикс DNS-имени** Введите URL-адрес, который пользователи должны использовать для веб-доступа к удаленным рабочим столам.
       - **Имя домена AD** Введите полное имя экземпляра Azure AD, например "contoso.onmicrosoft.com" или "contoso.com".
       - **Имя виртуальной сети AD** и **Имя подсети AD** Введите те же значения, которые вы использовали при создании виртуальной сети диспетчера ресурсов Azure. Это подсеть, к которой будут подключаться ресурсы служб удаленных рабочих столов.
       - **Имя пользователя администратора** и **Пароль администратора**: Введите учетные данные администратора, который является членом группы **Администраторы AAD DC** в Azure AD.

     - **Шаблон**
        - Удалите все свойства **dnsServers**: выбрав команду **Изменить шаблон** на странице шаблона быстрого запуска Azure найдите запись dnsServers и удалите свойство.

           Например, перед удалением свойства **dnsServers**:

           ![Шаблон быстрого запуска Azure со свойством dnsSettings](media/rds-remove-dnssettings-before.png)

           Здесь тот же файл после удаления свойства:

           ![Шаблон быстрого запуска Azure без свойства dnsSettings](media/rds-remove-dnssettings-after.png)

   - [Развертывание служб удаленных рабочих столов вручную](rds-deploy-infrastructure.md).

