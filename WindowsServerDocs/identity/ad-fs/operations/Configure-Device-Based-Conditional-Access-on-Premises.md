---
description: Дополнительные сведения см. в статье Настройка локального условного доступа с помощью зарегистрированных устройств.
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: Настройка локального условного доступа на основе устройств
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.openlocfilehash: 5b840243a7f17dc65db5d3c0605c3e5a321352f2
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049722"
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>Настройка локального условного доступа с помощью зарегистрированных устройств


Следующий документ поможет вам установить и настроить локальный условный доступ с зарегистрированными устройствами.

![условный доступ](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)

## <a name="infrastructure-pre-requisites"></a>Предварительные требования к инфраструктуре
Перед началом локального условного доступа необходимо выполнить следующие требования.

|Требование|Описание
|-----|-----
|Подписка Azure AD с Azure AD Premium | Для включения обратной записи устройства в локальный условный доступ — [Бесплатная пробная версия](https://azure.microsoft.com/trial/get-started-active-directory/)
|Подписка Intune|[Бесплатная пробная версия](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0) необходима только для интеграции с MDM для сценариев соответствия устройств.
|Azure AD Connect|Ноябрь 2015 QFE или более поздней версии.  Получить последнюю версию можно [здесь](https://www.microsoft.com/download/details.aspx?id=47594).
|Windows Server 2016|Сборка 10586 или более новая версия для AD FS
|Схема Active Directory Windows Server 2016|Требуется уровень схемы 85 или выше.
|Контроллер домена Windows Server 2016|Это требуется только для развертываний "Hello для бизнеса — доверие".  Дополнительные сведения можно найти [здесь](/windows/security/identity-protection/hello-for-business/hello-identity-verification).
|Клиент Windows 10|Сборка 10586 или более новая, присоединенная к указанному выше домену, требуется для присоединения к домену Windows 10 и Microsoft Passport for Work сценариев
|Учетная запись пользователя Azure AD с назначенной лицензией Azure AD Premium|Для регистрации устройства



## <a name="upgrade-your-active-directory-schema"></a>Обновление схемы Active Directory
Чтобы использовать локальный условный доступ с зарегистрированными устройствами, необходимо сначала обновить схему AD.  Должны быть выполнены следующие условия.
    - Схема должна быть версии 85 или более поздней.
    - Это требуется только для леса, к которому присоединен AD FS

> [!NOTE]
> Если вы установили Azure AD Connect до обновления до версии схемы (уровень 85 или выше) в Windows Server 2016, необходимо будет повторно запустить Azure AD Connect установку и обновить локальную схему AD, чтобы убедиться, что правило синхронизации для msDS-Кэйкредентиаллинк настроено.

### <a name="verify-your-schema-level"></a>Проверка уровня схемы
Чтобы проверить уровень схемы, выполните следующие действия.

1.  Можно использовать ADSIEdit или LDP и подключиться к контексту именования схемы.
2.  С помощью ADSIEdit правой кнопкой мыши щелкните "CN = Schema, CN = Configuration, DC = <domain> , DC = <com> и выберите пункт" Свойства ".  Релпаце домен и com-части с информацией о лесе.
3.  В редакторе атрибутов выберите атрибут Обжектверсион, и он сообщит вам о своей версии.

![Редактирование ADSI](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)

Можно также использовать следующий командлет PowerShell (замените объект сведениями о контексте именования схемы):

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion

```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png)

Дополнительные сведения об обновлении см. [в статье обновление контроллеров домена до Windows Server 2016](../../ad-ds/deploy/upgrade-domain-controllers.md).

## <a name="enable-azure-ad-device-registration"></a>Включение регистрации устройств Azure AD
Чтобы настроить этот сценарий, необходимо настроить функцию регистрации устройств в Azure AD.

Для этого выполните действия, описанные в разделе [Настройка присоединение к Azure AD в вашей организации](/azure/active-directory/devices/device-management-azure-portal) .

## <a name="setup-ad-fs"></a>AD FS установки
1. Создайте [новую ферму AD FS 2016](../deployment/deploying-a-federation-server-farm.md).
2.  Или [перенесите](../deployment/upgrading-to-ad-fs-in-windows-server.md) ферму в AD FS 2016 с AD FS 2012 R2
4. Развертывание [Azure AD Connect](../deployment/upgrading-to-ad-fs-in-windows-server.md) с использованием пользовательского пути для подключения AD FS к Azure AD.

## <a name="configure-device-write-back-and-device-authentication"></a>Настройка проверки подлинности при обратной записи устройства и устройства
> [!NOTE]
> Если вы выполняли Azure AD Connect с помощью стандартных параметров, правильные объекты Active Directory были созданы специально для вас.  Однако в большинстве AD FS сценариев Azure AD Connect был запущен с пользовательскими настройками для настройки AD FS, поэтому необходимо выполнить следующие действия.

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>Создание объектов AD для проверки подлинности устройств в AD FS
Если в вашей ферме AD FS еще не настроена проверка подлинности устройств (это можно проверить в консоли управления AD FS в разделе "Служба" -> "Регистрация устройств"), выполните следующие действия, чтобы создать верные объекты и конфигурацию AD DS.

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>Примечание. для приведенных ниже команд требуются средства администрирования Active Directory, поэтому если сервер федерации не является контроллером домена, сначала установите средства, используя шаг 1 ниже.  В противном случае можно пропустить этот шаг.

1.  Запустите мастер **добавления ролей и компонентов** и выберите компонент **Средства удаленного администрирования сервер** -> **Средства администрирования ролей** -> **Средства AD DS и AD LDS**, а затем выберите **Модуль Active Directory для Windows PowerShell** и **Средства AD DS**.

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)

2. На сервере-источнике AD FS Войдите в систему как AD DS пользователя с правами администратора предприятия и откройте командную строку PowerShell с повышенными привилегиями.  Затем выполните следующие команды PowerShell:

   `Import-module activedirectory`
   `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" `
3. Во всплывающем окне нажмите кнопку Да.

>Примечание. Если служба AD FS настроена для использования учетной записи GMSA, введите имя учетной записи в формате "домаин\аккаунтнаме $".

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)

Указанная выше команда PSH создает следующие объекты:


- Контейнер RegisteredDevices в разделе домена AD
- Контейнер и объект службы регистрации устройств в разделе "Настройка" --> "Службы" --> "Конфигурация регистрации устройств"
- Контейнер и объект DKM службы регистрации устройств в разделе "Настройка" --> "Службы" --> "Конфигурация регистрации устройств"

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)

4. После выполнения этой команды отобразится сообщение об успешном завершении.

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png)

###        <a name="create-service-connection-point-scp-in-ad"></a>Создание точки подключения службы (SCP) в AD
Если вы планируете использовать присоединение к домену Windows 10 (с автоматической регистрацией в Azure AD), как описано здесь, выполните следующие команды, чтобы создать точку подключения службы в AD DS
1.  Откройте Windows PowerShell и выполните следующую команду:

    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" `

>Примечание. при необходимости скопируйте файл Адсинкпреп. PSM1 с сервера Azure AD Connect.  Этот файл находится в каталоге Program Files\Microsoft Azure Active Directory Connect\AdPrep

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)

2. Укажите учетные данные глобального администратора Azure AD

    `PS C:>$aadAdminCred = Get-Credential`

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png)

3. Выполните следующую команду PowerShell

   `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred `

Где [AD connector account name] — имя учетной записи, которую вы настроили в Azure AD Connect при добавлении локального каталога AD DS.

После выполнения приведенных выше команд клиенты Windows 10 могут найти верный домен Azure AD для присоединения путем создания объекта serviceConnectionpoint в AD DS.

### <a name="prepare-ad-for-device-write-back"></a>Подготовка AD к обратной записи устройств
Чтобы обеспечить верное состояние объектов и контейнеров AD DS для обратной записи устройств из Azure AD, выполните следующие действия.

1.  Откройте Windows PowerShell и выполните следующую команду:

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] `

Где [AD connector account name] — имя учетной записи, которую вы настроили в Azure AD Connect при добавлении локального каталога AD DS в формате domain\accountname

Приведенная выше команда создает следующие объекты для обратной записи устройств в AD DS, если они еще не были созданы, и обеспечивает доступ к указанному имени учетной записи соединителя AD

- Контейнер RegisteredDevices в разделе домена AD
- Контейнер и объект службы регистрации устройств в разделе "Настройка" --> "Службы" --> "Конфигурация регистрации устройств"

### <a name="enable-device-write-back-in-azure-ad-connect"></a>Включение обратной записи устройств в Azure AD Connect
Включите обратную запись устройств в Azure AD Connect, если она еще не включена. Для этого запустите мастер еще раз и выберите **"Настройка параметров синхронизации"**, затем установите флажок обратной записи устройств и выберите лес, в котором выполнялись приведенные выше командлеты

### <a name="configure-device-authentication-in-ad-fs"></a>Настройка проверки подлинности устройств в AD FS
Используйте окно командной строки PowerShell с повышенными привилегиями для настройки политики AD FS путем выполнения следующей команды

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All`

### <a name="check-your-configuration"></a>Проверка конфигурации
Для справки ниже приведен полный список устройств, контейнеров и разрешений AD DS, необходимых для обратной записи и проверки подлинности устройств



- объект типа ms-DS-DeviceContainer в CN=RegisteredDevices,DC=&lt;домен&gt;
    - доступ для чтения к учетной записи службы AD FS
    - доступ для чтения и записи к учетной записи соединителя AD с синхронизацией Azure AD Connect</br></br>

- Контейнер CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=&lt;домен&gt;
- Контейнер DKM службы регистрации устройств под указанным выше контейнером

![Регистрация устройства](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png)



- объект типа serviceConnectionpoint в CN=&lt;guid&gt;, CN=Device Registration

- Configuration,CN=Services,CN=Configuration,DC=&lt;домен&gt;
  - доступ для чтения и записи к указанному имени учетной записи соединителя AD в новом объекте</br></br>


- Объект типа msDS-Девицерегистратионсервицеконтаинер в CN = Device Registration Services, CN = Конфигурация регистрации устройств, CN = Services, CN = Configuration, DC =&лтдомаин>


- объект типа msDS-DeviceRegistrationService в указанном выше контейнере

### <a name="see-it-work"></a>Просмотреть работу
Чтобы оценить новые утверждения и политики, сначала зарегистрируйте устройство.  Например, вы можете присоединить компьютер с Windows 10 к Azure AD с помощью приложения "Параметры" в разделе "система" — > о программе или настроить присоединение к домену Windows 10 с автоматической регистрацией устройств, [выполнив дополнительные действия.](/azure/active-directory/devices/hybrid-azuread-join-plan)  Сведения о присоединении устройств с Windows 10 Mobile см. в документе [здесь](/windows/client-management/join-windows-10-mobile-to-azure-active-directory).

Для простейшего ознакомления Войдите в AD FS с помощью тестового приложения, в котором отображается список утверждений. Вы сможете увидеть новые заявки, включая "управляемые", "трусттипе" и "не соответствует".  Если включить Microsoft Passport для работы, вы также увидите утверждение PRT.


## <a name="configure-additional-scenarios"></a>Настройка дополнительных сценариев
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>Автоматическая регистрация для компьютеров, присоединенных к домену Windows 10
Чтобы включить автоматическую регистрацию устройств для компьютеров, присоединенных к домену Windows 10, выполните шаги 1 [и 2.](/azure/active-directory/devices/hybrid-azuread-join-plan)
Это поможет вам получить следующие сведения:

1. Убедитесь, что точка подключения службы в AD DS существует и имеет необходимые разрешения (мы создали этот объект, но он не имеет вреда для двойной проверки).
2. Убедитесь, что AD FS настроен правильно
3. Убедитесь, что в системе AD FS установлены правильные конечные точки и настроены правила утверждений.
4. Настройка параметров групповой политики, необходимых для автоматической регистрации присоединенных к домену компьютеров

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work
Сведения о включении Windows 10 с Microsoft Passport for Work см [. в разделе включение Microsoft Passport for work в Организации.](/windows/security/identity-protection/hello-for-business/hello-identity-verification)

### <a name="automatic-mdm-enrollment"></a>Автоматическая регистрация MDM
Чтобы включить автоматическую регистрацию зарегистрированных устройств MDM, чтобы можно было использовать утверждение, соответствующее политике управления доступом, выполните действия, описанные [здесь.](/windows/client-management/join-windows-10-mobile-to-azure-active-directory)

## <a name="troubleshooting"></a>Устранение неполадок
1.  Если появляется сообщение об ошибке `Initialize-ADDeviceRegistration` о том, что объект уже существует в неправильном состоянии, например "объект службы DRS был найден без всех обязательных атрибутов", возможно, вы уже выполнили Azure AD Connect команды PowerShell, а также частичную конфигурацию в AD DS.  Попробуйте удалить вручную объекты в разделе **CN = Device Registration Configuration, CN = Services, CN = Configuration, DC = &lt; domain &gt;** и повторите попытку.
2.  Для клиентов, присоединенных к домену Windows 10
    1. Чтобы проверить, работает ли проверка подлинности устройства, войдите на клиент, присоединенный к домену, в качестве тестовой учетной записи пользователя. Чтобы быстро запустить подготовку, заблокируйте и разблокируйте Рабочий стол по крайней мере один раз.
    2. Инструкции по проверке связи учетных данных ключа СТК для объекта AD DS (синхронизация по-прежнему должна выполняться дважды?)
3.  При получении сообщения об ошибке при попытке зарегистрировать компьютер Windows, на котором устройство уже зарегистрировано, но вы не можете или уже отменяли регистрацию устройства, в реестре может быть фрагмент конфигурации регистрации устройства.  Чтобы исследовать и удалить это, выполните следующие действия.
    1. На компьютере Windows откройте редактор реестра и перейдите по адресу **хклм\софтваре\микрософт\енроллментс** .
    2. В этом разделе в форме GUID будет много подразделов.  Перейдите к подразделу, который содержит ~ 17 значений и имеет "Енроллменттипе" из "6" [присоединено к MDM] или "13" (присоединенные к Azure AD).
    3. Изменить **енроллменттипе** на **0**
    4. Попробуйте зарегистрировать устройство или повторить регистрацию

### <a name="related-articles"></a>Похожие статьи
* [Защита доступа к Office 365 и другим приложениям, подключенным к Azure Active Directory](/azure/active-directory/conditional-access/overview)
* [Политики условного доступа к службам Office 365 с устройств](/azure/active-directory/conditional-access/overview)
* [Настройка локального условного доступа с помощью регистрации устройств в Azure Active Directory](/azure/active-directory/active-directory-device-registration-on-premises-setup)
* [Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10](/azure/active-directory/devices/hybrid-azuread-join-plan)
